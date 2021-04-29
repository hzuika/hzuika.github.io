[INDEX](../)  

# Blender と IME

## Windows

2021年04/18時点で，Windows版Blenderはプロパティを変更するボタンでのみ日本語入力が可能です(IMEが利用可能)．
テキストエディタ，コンソール，フォントオブジェクトでは日本語入力ができません．
これまでにBlenderの開発者は何度かIMEサポートのためのパッチを提出しましたが，正式に採用されませんでした．
2020年2月に提出されたIMEをサポートするパッチ[D6861](https://developer.blender.org/D6861)は，
途中で内容が変更され，現在は，韓国語をサポートするのみとなっています．
このページでは[D6861](https://developer.blender.org/D6861)パッチを，
現在の最新版のBlenderに適用していく過程で気づいたこと，学んだことを載せていく個人的なメモになります．
いくつか問題が残っているため，それらの解決方法についても記載していく予定です．

## wmNotifier

masterブランチで調査します．  
```
git checkout master
```

`source\blender\windowmanager\intern\wm_event_system.c` 542行目で`wm->notifier_queue`から，`wmNotifier`を取得しています．

```cpp
  wmNotifier *note;
  while ((note = BLI_pophead(&wm->notifier_queue))) {
    LISTBASE_FOREACH (wmWindow *, win, &wm->windows) {
```

`wm`は438行目で引数の`bContext *C`から取得しています．

```cpp

  wmWindowManager *wm = CTX_wm_manager(C);
  if (wm == NULL) {
```

579行目の反復文が，580行目の条件文で飛ばされるため，593行目の関数が実行されません．
そのため，ウィンドウ描画のタグがつけられず(`do_draw = false`のまま)，IME入力時に変換前文字列がウィンドウに描画されません．

```cpp
          if ((note->category == NC_SPACE) && note->reference) {
            /* Filter out notifiers sent to other spaces. RNA sets the reference to the owning ID
             * though, the screen, so let notifiers through that reference the entire screen. */
            if (!ELEM(note->reference, area->spacedata.first, screen)) {
              continue;
            }
          }
/* ... */
          ED_area_do_listen(&area_params);
```

`NC_SPACE`の定義が記述されている`WM_types.h`にコメントが記載されています．

```cpp
/* When passing a space as reference data with this (e.g. `WM_event_add_notifier(..., space)`),
 * the notifier will only be sent to this space. That avoids unnecessary updates for unrelated
 * spaces. */
#define NC_SPACE (15 << 24)
```

これを使ってスペースを参照データとして渡す場合（例えば `WM_event_add_notifier(..., space)`）、通知はこのスペースにのみ送られます。 そうすることで、関係のないスペースの不必要な更新を避けることができます。

`WM_event_add_notifier`で検索すると，`source\blender\editors\space_text\text_ops.c`の3466行目の`text_insert_exec`関数内で使用されていました．

```cpp
  WM_event_add_notifier(C, NC_TEXT | NA_EDITED, text);
```

タグの再描画に関しては，`source\blender\editors\interface\interface_handlers.c`の`ui_do_but_textedit`関数内で3854行目に`ED_region_tag_redraw`が使われていました．IME処理中(`WM_IME_COMPOSITE_START`か`WM_IME_COMPOSITE_EVENT`，`WM_IME_COMPOSITE_END`)は`changed`が`true`になります．
```cpp
  if (changed || (retval == WM_UI_HANDLER_BREAK)) {
    ED_region_tag_redraw(data->region);
  }
```

IMEパッチの`text_insert_modal`でも同じような処理を入れてみました．
ウィンドウに表示されるようになりました．

Console と Font Curveについても同じように変更していきます．
* Consoleでは表示されませんでした．
* Font Curveでも表示されませんでした．

---

このパッチだと，検索フィルタに日本語が入力できないので調査が必要です．
(公式版だと入力できるので，不必要な変更が行われている可能性が高いです．)
```python
bpy.context.space_data.search_filter = ""
```

interfaceの変更点を確認して，このパッチだと，IME処理をどのように進めているのか理解する必要があります．

---

2021-04-29 17:48:37

`intern\ghost\intern\GHOST_SystemWin32.cpp`

Windows API で定義されたメッセージ
ウィンドウからアプリケーションへ送信されたメッセージにしたがって処理を行う
```cpp
LRESULT WINAPI GHOST_SystemWin32::s_wndProc(HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam)
{
  /* ... */
WM_IME_SETCONTEXT // ウィンドウアクティブ時に送信

WM_IME_STARTCOMPOSITION // コンポジション文字列生成前に送信
  // m_dataにeventImeDataを追加したGHOST_kEventImeCompositionStartイベント追加

WM_IME_COMPOSITION // コンポジション状態変更時に送信
  // m_dataにeventImeDataを追加したGHOST_kEventImeCompositionイベント追加

WM_IME_ENDCOMPOSITION // コンポジション終了時に送信
  // m_dataにeventImeDataを追加したGHOST_kEventImeCompositionEndイベント追加
/* ... */
}
```
[入力方式マネージャーのメッセージ - Win32 apps | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/win32/intl/input-method-manager-messages)
[WM_IME_SETCONTEXT メッセージ (Winuser. h) - Win32 apps | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/win32/intl/wm-ime-setcontext)
[WM_IME_STARTCOMPOSITION メッセージ (Winuser. h) - Win32 apps | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/win32/intl/wm-ime-startcomposition)
[WM_IME_ENDCOMPOSITION メッセージ (Winuser. h) - Win32 apps | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/win32/intl/wm-ime-endcomposition)

`s_wndProc`は`lpfnWndProc`に代入すると，ウィンドウから送られるメッセージを処理してくれる．

---

アプリケーション(Ghost)の処理

`source\blender\windowmanager\intern\wm_event_system.c`

```cpp
/**
 * Windows store own event queues #wmWindow.event_queue (no #bContext here).
 */
void wm_event_add_ghostevent(wmWindowManager *wm, wmWindow *win, int type, void *customdata)
{
  /* ... */
GHOST_kEventImeCompositionStart
  // win->ime_dataにcustomdataを追加して，WM_IME_COMPOSITE_STARTイベントを追加
GHOST_kEventImeComposition
  // WM_IME_COMPOSITE_EVENTイベントを追加
GHOST_kEventImeCompositionEnd
  // WM_IME_COMPOSITE_ENDイベントを追加
  /* ... */
}
```

UIボタンでのIMEテキスト編集の処理
`source\blender\editors\interface\interface_handlers.c`
```cpp
static void ui_do_but_textedit(
    bContext *C, uiBlock *block, uiBut *but, uiHandleButtonData *data, const wmEvent *event)
{
  /* ... */
WM_IME_COMPOSITE_START
  // 選択範囲の削除
WM_IME_COMPOSITE_EVENT
  // data->strにime_data->str_resultテキスト挿入
  // IME確定変換文字列(str_result)のみで，変換中文字列(str_composite)は描画処理のみ
WM_IME_COMPOSITE_END
  /* ... */
}
```

UIボタンでのIME変換中文字列，カーソル，下線の描画
`source\blender\editors\interface\interface_widgets.c`


```cpp
static void widget_draw_text(const uiFontStyle *fstyle,
                             const uiWidgetColors *wcol,
                             uiBut *but,
                             rcti *rect)
{
  /* ... */

      /* FIXME, IME is modifying 'const char *drawstr! */
      ime_data = ui_but_ime_data_get(but);
      // but->active->window->ime_dataを取得

      if (ime_data && ime_data->composite_len) {
        /* insert composite string into cursor pos */
        BLI_snprintf((char *)drawstr,
                     UI_MAX_DRAW_STR,
                     "%s%s%s",
                     but->editstr,
                     ime_data->str_composite,
                     but->editstr + but->pos);
      }
  /* ... */
}
```

---

`ui_textedit_begin`と`ui_textedit_end`時のIME有効/無効処理