[INDEX](../)

このページでは，遭遇したエラーとその対処法について載せていきます．

## サービスの作成に失敗しました listen EACCES: permission denied 0.0.0.0:52330
発生日:2021-04-18 16:12:30<br/>
Visual Studio Code で 拡張機能 Open In Default Browser(peakchen90.open-html-in-browser) を
使用する際に発生．以前までは通常に使用できた．

vscode で show Log の Window を選択すると以下のエラーメッセージ<br/>
```
[2021-04-18 16:23:06.076] [renderer3] [error] listen EACCES: permission denied 0.0.0.0:52336: Error: listen EACCES: permission denied 0.0.0.0:52336
at Server.setupListenHandle [as _listen2] (net.js:1296:21)
at listenInCluster (net.js:1361:12)
at Server.listen (net.js:1447:7)
at LocalServer.<anonymous> (c:\Users\hashi\.vscode\extensions\peakchen90.open-html-in-browser-2.1.3\dist\extension.js:123:25)
at Generator.next (<anonymous>)
at fulfilled (c:\Users\hashi\.vscode\extensions\peakchen90.open-html-in-browser-2.1.3\node_modules\tslib\tslib.js:107:62)
at runMicrotasks (<anonymous>)
at processTicksAndRejections (internal/process/task_queues.js:97:5)
```

ポート番号が使われていて，エラーが発生している可能性がある．
Pythonで同じポートの http server を立てようとして<b>OSError: [WinError 10013] アクセス許可で禁じられた方法でソケットにアクセスしようとしました。</b>と出たのでその可能性が高い．
### 一時的措置
Python で http server を立てる．

---

## 作成したhtmlをブラウザで開くと文字化けする
文字コードを設定する必要がある．
### 解決
```html
  <head>
    <meta charset="utf-8"/>
  </head>
```
