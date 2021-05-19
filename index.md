# なぜ Mac の Blender は日本語入力ができないの?

## Markded Text は下線を引くなど、修飾を行うテキスト

## `setMarkedText` と `insertText` の違い
MarkedTextが変更される可能性のあるテキスト（composing text)で，insertTextは確定後のテキスト

keyDown メソッドで送られてくるイベントはIMEがOFFでもONでも同じである．

NSUnderline 1が細い下線，2が太い下線

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
