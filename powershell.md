コマンド履歴をコピー
```powershell
Get-History | ForEach-Object {$_.CommandLine} | clip
```

コマンド履歴の削除
```powershell
Clear-History
```

ファイル名をコピー
```powershell
ls -Name | clip
```