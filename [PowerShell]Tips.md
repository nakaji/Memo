# PowerShellメモ

### スクリプト自身のパス
	$MyInvocation.MyCommand.Path

### スクリプトが格納されているパスを返す
	Split-Path $MyInvocation.MyCommand.Path

### nullとの比較
	$hoge -eq $null

### ファイルの一覧取得
	#指定したファイル,ディレクトリ
	Get-Item .
	#指定したディレクトリ配下のファイル,ディレクトリ
	Get-ChildItem . -Recurse

### 環境変数の取得
	Get-ChildItem env:
	$env:CLASSPATH

### 実行確認
	$typename = "Management.Automation.Host.ChoiceDescription"
	$yes = New-Object $typename("&Yes","実行する")
	$no = New-Object $typename("&NO","実行しない")
	$choice = [Management.Automation.Host.ChoiceDescription[]]($yes, $no)
	$answer = $Host.UI.PromptForChoice("<実行確認>","実行しますか？", $choice, 0)
	if ($answer -ne 0) { return }


##文字列操作
###文字列配列の結合
	[string]::Join("-", $a)

###文字列の置換
正規表現使用可能（エスケープ文字は\）

	"hogefuga" -replace "^hoge","piyo"

Stringオブジェクトのメソッドで行う

	"hogefuga".Replace("hoge", "piyo")
