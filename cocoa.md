こちらをコンパイル．
[Minimal cocoa text entry for OpenGL apps](https://gist.github.com/MasonRemaley/af5e1d3c538aedbfd6c726762205b1fb)

英数字入力と，IME確定後文字列をコンソールに出力するプログラム．

プロトコル `NSTextInputClient` はメソッドの宣言だけされていて，実装は継承先依存．

`-`はインスタンスメソッド

`BOOL`は`YES`か`NO`

`:`のあとが引数
第二引数以降は`ラベル:引数`
`[クラスインスタンス メソッド: 引数]`

Objective-Cクラスインスタンスの自動解放
```objective-c
    @autoreleasepool {
    }
```

---

NSTextInputClient

> https://developer.apple.com/documentation/appkit/nstextinputclient
  
> テキストインプットマネジメントシステムとインタラクトするためにテキストビューが実装しなければならないメソッドのセット

---

> [IMEを使う（macOS編） - Qiita](https://qiita.com/496_/items/4ad166f4104d0bb24e80)

> [Cocoa で独自の Text View を実装する](https://metareal.blog/2008/11/08/cocoa-custom-text-view/)