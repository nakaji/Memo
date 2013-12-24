#PowerShellメモ

###スクリプト自身のパス
	$MyInvocation.MyCommand.Path

###スクリプトが格納されているパスを返す
	Split-Path $MyInvocation.MyCommand.Path

###nullとの比較
	$hoge -eq $null

###ファイルの一覧取得
	#指定したファイル,ディレクトリ
	Get-Item .
	#指定したディレクトリ配下のファイル,ディレクトリ
	Get-ChildItem . -Recurse

###環境変数の取得
	Get-ChildItem env:
	$env:CLASSPATH

##文字列操作
###文字列配列の結合
	[string]::Join("-", $a)

###文字列の置換
正規表現使用可能（エスケープ文字は\）

	"hogefuga" -replace "^hoge","piyo"

Stringオブジェクトのメソッドで行う

	"hogefuga".Replace("hoge", "piyo")
