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


[sharedApplication | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nsapplication/1428360-sharedapplication)

[setActivationPolicy: | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nsapplication/1428621-setactivationpolicy?language=objc)

[initWithContentRect:styleMask:backing:defer: | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nswindow/1419477-initwithcontentrect?language=objc)

[NSMakeRect(_:_:_:_:) | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/1391329-nsmakerect)

[NSWindowStyleMask | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nswindowstylemask?language=objc)

[NSBackingStoreType | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nsbackingstoretype?language=objc)

[cascadeTopLeftFromPoint: | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nswindow/1419392-cascadetopleftfrompoint?language=objc)

[makeKeyAndOrderFront(_:) | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nswindow/1419208-makekeyandorderfront)

[activateIgnoringOtherApps: | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nsapplication/1428468-activateignoringotherapps?language=objc)

[(旧) Cocoaの日々: ウィンドウを前へ、前へ、一番前へ](http://xcatsan.blogspot.com/2009/02/blog-post_12.html)

[run | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nsapplication/1428631-run?language=objc)

---

NSTextInputClient

> https://developer.apple.com/documentation/appkit/nstextinputclient
  
> テキストインプットマネジメントシステムとインタラクトするためにテキストビューが実装しなければならないメソッドのセット

---

> [IMEを使う（macOS編） - Qiita](https://qiita.com/496_/items/4ad166f4104d0bb24e80)

> [Cocoa で独自の Text View を実装する](https://metareal.blog/2008/11/08/cocoa-custom-text-view/)

> [NSTextInputClient | Apple Developer Documentation](https://developer.apple.com/documentation/appkit/nstextinputclient/)

> [マルチプラットフォームでIME対応させたいメモ - Qiita](https://qiita.com/shibukawa/items/add9a4bb1b1f959aa1fb)

> [glfwマルチプラットフォームでのIME対応の困りごとまとめ - Qiita](https://qiita.com/shibukawa/items/54334954b755e16a0863)

> [Mac/API/NSTextInputClientメモ - wxStyledTextCtrlでの日本語入力 @ ウィキ - atwiki（アットウィキ）](https://w.atwiki.jp/wximsupport/pages/35.html)