# なぜ Mac の Blender は日本語入力ができないの?

## Markded Text は下線を引くなど、修飾を行うテキスト

## `setMarkedText` と `insertText` の違い
MarkedTextが変更される可能性のあるテキスト（composing text)で，insertTextは確定後のテキスト

keyDown メソッドで送られてくるイベントはIMEがOFFでもONでも同じである．

### BlenderのkeyDown時
[event characters]
[event charactersIgnoringModifiers]
はどちらも同じ英数字．
[self inputContext]は存在する．
[self interpretKeyEvents:events]を実行できるようにしたら， setMarkedTextとinsertTextが正常に働いていた．
しかし，blender上には表示されていない．
そのため，macOS Cocoa -> GHOST -> Window Manager -> Blender上の表示 まで文字列情報を渡していく必要がある．

keyDownでは最初にsystemCocoa->handleKeyEventsが実行されてしまうので，IME ON時には実行しないようにする．
handleKeyEventsによって，GHOST_EventKeyのGHOST_kEventKeyDownタイプをpushEventしている．
GHOST_kEventKeyDownタイプのイベントはwm_event_system.cのwm_event_add_ghosteventでGHOST_TEventKeyDataから，wmEventに変わり，wm_event_addで追加される(win->event_queueに追加)．
event_queueはwm_event_system.cのwm_event_do_handlersで適宜処理される．
wmEventが各関数の引数として渡されて，wmEventのevent->utf8_bufによって取得される．

NSUnderline 1が細い下線，2が太い下線

NSMarkedClauseSegment が変換単位

IME OFF中はsetMarkedTextが呼ばれない．

IME 変換確定時(Enterを押したとき)にinsertTextが呼ばれる．
insertTextはIME OFF中も呼ばれる．

blender の insertText はIME OFF時でも呼ばれていない

blender実行中
```
2021-05-20 03:05:25.268 Blender[13677:888528] *** ProcessInputSourceSwitchEventCandidate - Japanese IM (<TSMInputSource 0x119614b00> Input Mode: com.apple.inputmethod.Japanese (Parent = com.apple.inputmethod.Kotoeri.RomajiTyping)) is not handling inEventKind(1) inKeyCode(104)*** BAIL kana/eisu handling
```

## Windows IME on Blender
WM_IME_SETCONTEXT メッセージのタイミング
* blenderウィンドウがアクティブ(画面内クリック)
* blenderウィンドウが非アクティブ(画面外クリック)
* UIボタンの日本語入力確定後のさらに次のEnterでフォーカスがUIボタンから外れた時2回

WM_IME_STARTCOMPOSITION メッセージのタイミング
* IME ONで最初にキーを押したとき．

WM_IME_COMPOSITION メッセージのタイミング
* 押し初めに3回
* 二文字目から2回
* BackSpaceで文字が残っていると2回，なくなると1回
* 矢印キーで1回

WM_END_COMPOSITION メッセージのタイミング
* 変換前文字がなくなるとき

### 旧IMEの場合，
* GHOST_kEventImeCompositionStart
* GHOST_kEventImeComposition 
* GHOST_kEventImeCompositionEnd
も同じ数だけ出ている．

sel_start, sel_end はIMEコンポジション文字列中の変換対象の範囲．（特に下線が太くなる部分)
Unicodeで表したときのバイト数なので，Asciiが1 byte éなどの拡張ラテン文字が2 byte 日本語がおよそ3 byte
絵文字が 4 byte (fontが対応していても，blenderでは表示されない．)
backspaceでコンポジション文字列を全て消すと，sel_startとsel_endはどちらも -1 になる．

```
WM_IME_STARTCOMPOSITION
WM_IME_COMPOSITION
GHOST_kEventImeCompositionStart
GHOST_kEventImeComposition
sel_start, 0
sel_end, 3
ime composition, あ
WM_IME_COMPOSITION
GHOST_kEventImeComposition
sel_start, 0
sel_end, 3
ime composition, あ
WM_IME_COMPOSITION
GHOST_kEventImeComposition
sel_start, 0
sel_end, 3
ime composition, あ
```

最初にIMEで入力したとき 1回目は GHOST_kEventKeyDown イベントが発生しない．
2文字目以降の入力では 対応するキーの GHOST_kEventKeyDown イベントが発生している．
ただし，kEventKeyDown イベントによって，半角文字が勝手に入力されることはない．

```
WM_IME_STARTCOMPOSITION
WM_IME_COMPOSITION
GHOST_kEventImeCompositionStart
GHOST_kEventImeComposition
ime composition, あ
WM_IME_COMPOSITION
GHOST_kEventImeComposition
ime composition, あ
WM_IME_COMPOSITION
GHOST_kEventKeyDown, i
GHOST_kEventImeComposition
ime composition, あい
WM_IME_COMPOSITION
GHOST_kEventImeComposition
ime composition, あい
WM_IME_COMPOSITION
GHOST_kEventImeComposition
ime composition, あい
WM_IME_COMPOSITION
WM_IME_ENDCOMPOSITION
GHOST_kEventImeComposition
GHOST_kEventImeCompositionEnd
```


### 新IMEの場合，
最初に入力したとき，
* GHOST_kEventImeComposition 
が3回ではなく，1回だけ．
エラー 半角で入力されてから，IME入力が始まる．
keyDownイベントが発生している?

最初にIMEで入力したとき 1回目に GHOST_kEventKeyDown イベントが発生している．
この文字が最初に入力されている．
2文字目以降の入力では 対応するキーの GHOST_kEventKeyDown イベントが発生している．
ただし，kEventKeyDown イベントによって，半角文字が勝手に入力されることはない．

```
GHOST_kEventKeyDown, a
WM_IME_STARTCOMPOSITION
WM_IME_COMPOSITION
GHOST_kEventImeCompositionStart
GHOST_kEventImeComposition
ime composition, あ
GHOST_kEventKeyDown, i
WM_IME_COMPOSITION
GHOST_kEventImeComposition
ime composition, あい
GHOST_kEventKeyDown, 
WM_IME_COMPOSITION
WM_IME_ENDCOMPOSITION
GHOST_kEventImeComposition
GHOST_kEventImeCompositionEnd
```

### Google 日本語入力の場合，
* GHOST_kEventImeComposition は1回だけ

```
WM_IME_STARTCOMPOSITION
WM_IME_COMPOSITION
GHOST_kEventImeCompositionStart
GHOST_kEventImeComposition
ime composition, あ
WM_IME_COMPOSITION
GHOST_kEventKeyDown, i
GHOST_kEventImeComposition
ime composition, あい
WM_IME_COMPOSITION
WM_IME_ENDCOMPOSITION
GHOST_kEventImeComposition
GHOST_kEventImeCompositionEnd
```

## Win API を使用してIMEの調査
### New Microsoft IME
IME切り替えをキーボードから行うと，ImmGetOpenStatusでON/OFFがわかる．
しかし，IMEの入力モードのボタン(ツールバー)をクリックして切り替えると変わらない．
これは，WM_INPUT時でもWM_IME_NOTIFY時でも同じ．
しかし，クリックしたときに，WM_IME_NOTIFYの通知は来ているので，ここから推定できないものか
A  の状態でクリックして あ IME_SETOPENSTATUS -> でもGetOpenStatusは変わらないのでは?
あ の状態でクリックして A  IME_SETCONVERSIONMODE
それ以降はクリックだと IME_SETCONVERSIONMODE -> GetConversionMode ?
キーボードによるトグル IME_SETOPENSTATUS

GetKeyState(VK_KANA); はローマ字入力0，かな入力1だった．
かな入力時も，Aキーで ち を打つと，ﾁち とでてきた．


## NSTextInputClientプロトコルで実装した関数はどの順番で呼ばれているのか?
## selection range はどこなのか?

## Blender Windows IME
### 「あい」と入力したときの挙動．
#### Old Microsoft IME
```
GHOST_kEventKeyDown, i
```
#### New Microsoft IME
```
GHOST_kEventKeyDown, a
GHOST_kEventKeyDown, i
```
#### Google 日本語入力
```
GHOST_kEventKeyDown, i
```

---


#### Old Microsoft IME
```
WM_INPUT
WM_INPUT

WM_INPUT
GHOST_kEventKeyDown, i
WM_INPUT
```
#### New Microsoft IME
```
WM_INPUT
GHOST_kEventKeyDown, a
WM_INPUT

WM_INPUT
GHOST_kEventKeyDown, i
WM_INPUT
```

#### Google 日本語入力
```
WM_INPUT
WM_INPUT

WM_INPUT
GHOST_kEventKeyDown, i
WM_INPUT
```

---

Google 日本語入力も WM_INPUT で utf8_char の a は入力されている．

WM_IME_STARTCOMPOSITION の通知が来たら， GHOST_kEventKeyDown を消している．
Google 日本語入力と Old Microsoft IME では GHOST_kEventKeyDown より前にこれが行われているのでOK
New Microsoft IME では GHOST_kEventKeyDown の後に WM_IME_STARTCOMPOSITION が来ているのでKeyDownが消されずに通過してしまう．
```cpp
// GHOST_SystemWin32.cpp
        case WM_IME_STARTCOMPOSITION: {
          printf("WM_IME_STARTCOMPOSITION\n");
          GHOST_ImeWin32 *ime = window->getImeInput();
          eventHandled = true;
          /* remove input event before start comp event, avoid redundant input */
          eventManager->removeTypeEvents(GHOST_kEventKeyDown, window);
          ime->CreateImeWindow(hwnd);
          ime->ResetComposition(hwnd);
          event = processImeEvent(GHOST_kEventImeCompositionStart, window, &ime->eventImeData);
          break;
        }
```

A 半角英数(直接入力)
IME ON から OFF にすると設定が変わらない?
fullshape hiragana native roman
fullshape hiragana native
fullshape katakana native
fullshape hiragana alphanumeric
halfshape katakana native
halfshape hiragana alphanumeric roman
halfshape hiragana alphanumeric
あ
fullshape hiragana native
カ
fullshape katakana native
ｶ
halfshape katakana native
## Reference

https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/TextUILayer/Tasks/CreatingATextView.html

https://developer.apple.com/documentation/appkit/nstextinput

https://developer.apple.com/documentation/appkit/nstextinputclient

[Text Editing](https://developer.apple.com/library/archive/documentation/TextFonts/Conceptual/CocoaTextArchitecture/TextEditing/TextEditing.html)

https://github.com/blender/blender/blob/master/intern/ghost/intern/GHOST_WindowViewCocoa.h

https://github.com/blender/blender/blob/594f47ecd2d5367ca936cf6fc6ec8168c2b360d0/intern/ghost/intern/GHOST_WindowCocoa.mm#L285

https://github.com/blender/blender/blob/594f47ecd2d5367ca936cf6fc6ec8168c2b360d0/intern/ghost/intern/GHOST_WindowCocoa.mm#L366

Godot は GLFW のソースコードをもとにしているらしい．
[Implement NSTextInputClient protocol for IME · godotengine/godot@8aa86cb](https://github.com/godotengine/godot/commit/8aa86cb9bcb5db8a1909d4b1595e90dbffbff11e)

[Add IME support (macOS) by bruvzg · Pull Request #10142 · godotengine/godot](https://github.com/godotengine/godot/pull/10142)

[マルチプラットフォームでIME対応させたいメモ - Qiita](https://qiita.com/shibukawa/items/add9a4bb1b1f959aa1fb)

[NSTextInputClientでカーソル（キャレット？）表示関連の処理](https://gist.github.com/Axeryok/93a41481e3ebb7ff27da4bb8ec39c164)

[IMEを使う（macOS編） - Qiita](https://qiita.com/496_/items/4ad166f4104d0bb24e80)

[Mac/API/NSTextInputClientメモ - wxStyledTextCtrlでの日本語入力 @ ウィキ - atwiki（アットウィキ）](https://w.atwiki.jp/wximsupport/pages/35.html)

https://github.com/blender/blender/commit/4c43a14b9f61e9e8a049299278773699fc6d7b1d

[vimr/notes-on-cocoa-text-input.md at dd66d8e966c4935c4773045429ee5a5bd1e56f84 · qvacua/vimr](https://github.com/qvacua/vimr/blob/dd66d8e966c4935c4773045429ee5a5bd1e56f84/docs/notes-on-cocoa-text-input.md)

[chromium/index.md at d7da0240cae77824d1eda25745c4022757499131 · chromium/chromium](https://github.com/chromium/chromium/blob/d7da0240cae77824d1eda25745c4022757499131/docs/ui/input_event/index.md#L241)

[MacViews: Implement text input. · chromium/chromium@0282b03](https://github.com/chromium/chromium/commit/0282b03c86d52533c58af2c6e8de4c7bc7a89155)

[xi-mac/frontend.md at 6ce150ab185c3a5058d1440b6972c4a4fe252201 · xi-editor/xi-mac](https://github.com/xi-editor/xi-mac/blob/6ce150ab185c3a5058d1440b6972c4a4fe252201/doc/frontend.md)

[CocoaProgrammaticHowtoCollection/README.md at 2a2611cc751a1a7784570efae57e86adf40c29bb · eonil/CocoaProgrammaticHowtoCollection](https://github.com/eonil/CocoaProgrammaticHowtoCollection/blob/2a2611cc751a1a7784570efae57e86adf40c29bb/README.md)

[About the Cocoa Text System](https://developer.apple.com/library/archive/documentation/TextFonts/Conceptual/CocoaTextArchitecture/Introduction/Introduction.html)

# Blender の cpp ファイルではstd::coutが使えないのでprintfを使ったほうが無難．
# GitHub で tag はどのように使うの?
## iOS Chrome の GitHub でファイルを直接編集した時のコミットには tag をつけられない

# Google の拡張機能はどうやって自作するの?

# スマートフォンでテキストファイルを編集できる最も良い方法は?

# 正規分布をsvgで描く方法は?
## 正規分布をベジエ曲線で描く方法は?

# Zotero のメモのフォントを変える方法は?
## Reference
[【令和最新版】文献管理ソフト Zoteroのすゝめ｜SD｜note](https://note.com/sdeso/n/n013952313c1b)
## 行間隔がもう少し広いフォントに変える．

# R言語を VScode で使う方法は?

# 名詞 in which 動詞
名詞 which 動詞 in で名詞を修飾する。
whichが名詞の代わりになりながら、後の文と合わせて修飾文にする。
前置詞inは名詞の前に置きたいので、名詞の代わりのwhichの前に置く。


# as は when より同時に起こっている感じが強い

# tag 機能を実装するには?
データベースを使う方法としてTOXI法というものがあるらしい．
