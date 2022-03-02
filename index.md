# Profile

* [Zenn](https://zenn.dev/hzuika)

# Blenderへのコミット

* [Fix some shortcut keys not working on macOS with Japanese input](https://developer.blender.org/rB7336af325937)
  * macOSで日本語入力時に一部のショートカットキーが動かないバクの修正
* [Fix text object inserting multiple characters with a selection](https://developer.blender.org/rB8830cfe54160)
  * テキストオブジェクトで選択範囲に複数の文字を挿入する際のバグの修正 
* [Cleanup: correct the comment in ghost](https://developer.blender.org/rB22bef356aedd)
  * ソースコード内のコメントの修正
* [macOS: support Chinese and Korean input for text buttons](https://developer.blender.org/rB0ef794b5534a)
  * macOSでテキストボタン内の中国語入力と韓国語入力の実装
* [macOS: support Japanese input for text buttons](https://developer.blender.org/rB83e2f8c993dc)
  * macOSでテキストボタン内の日本語入力を実装
* [Fix: macOS wrong IME candidate window position on first display](https://developer.blender.org/rBac1ed19eaefe)
  * macOSでIME入力開始時の変換ウィンドウが正しい位置に表示されないバグの修正
* [Fix: IME conversion candidate window not correctly placed on macOS](https://developer.blender.org/rB2d0b9faaf6ec)
  * macOSでIMEの変換ウィンドウが正しい位置に表示されないバグの修正
* [Fix: IME input displays text after cursor before cursor](https://developer.blender.org/rB32124b940ee6)
  * IME使用時に，カーソルの後ろの文字がカーソルの前に表示されるバグの修正
* [Cleanup: replace NSTextInput with NSTextInputClient](https://developer.blender.org/rB2c6c1b6cc046)
  * 非推奨の`NSTextInput`プロトコルから`NSTextInputClient`プロトコルへ変更
* [Cleanup: use arrayWithObject to reduce the code](https://developer.blender.org/rBc1ba68dd042c)
  * Objective-C のコードを糖衣構文を使って行数削減
