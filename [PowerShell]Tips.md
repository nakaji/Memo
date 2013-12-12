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
