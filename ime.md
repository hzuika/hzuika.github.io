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
いくつか重大な問題が残っているため，それらの解決方法についても記載していく予定です．

## wmNotifier

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