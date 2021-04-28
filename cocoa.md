こちらをコンパイル．
[Minimal cocoa text entry for OpenGL apps](https://gist.github.com/MasonRemaley/af5e1d3c538aedbfd6c726762205b1fb)

英数字入力と，IME確定後文字列をコンソールに出力するプログラム．

プロトコル `NSTextInputClient` はメソッドの宣言だけされていて，実装は継承先依存．

`-`はインスタンスメソッド

`BOOL`は`YES`か`NO`

`:`のあとが引数
`[クラスインスタンス メソッド: 引数]`

Objective-Cクラスインスタンスの自動解放
```objective-c
    @autoreleasepool {
    }
```