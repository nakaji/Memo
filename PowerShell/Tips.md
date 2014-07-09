# PowerShellメモ
### プロファイル
	$profile

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

### プログラムの終了コード
	$lastexitcode

### スクリプトの終了コードを返す
	powershell -File ".\hoge.ps1"
	
### 環境変数の取得
	Get-ChildItem env:
	$env:CLASSPATH

### 実行確認（プロンプト）
	$typename = "Management.Automation.Host.ChoiceDescription"
	$yes = New-Object $typename("&Yes","実行する")
	$no = New-Object $typename("&NO","実行しない")
	$choice = [Management.Automation.Host.ChoiceDescription[]]($yes, $no)
	$answer = $Host.UI.PromptForChoice("<実行確認>","実行しますか？", $choice, 0)
	if ($answer -ne 0) { return }

## ファイル操作
### BOMなしのUTF8で出力する
    $encoding = New-Object System.Text.UTF8Encoding($False)
    [System.IO.File]::WriteAllLines("hoge.txt", $contents, $encoding);

### ディレクトリかどうかの判定
	if ($_.PSIsContainer) { }

## 文字列操作
### 文字列配列の結合
	[string]::Join("-", $a)

### 文字列の置換
正規表現使用可能（エスケープ文字は\）

	"hogefuga" -replace "^hoge","piyo"	#大文字小文字区別しない
	"hogefuga" -creplace "^hoge","piyo"	#大文字小文字区別する

Stringオブジェクトのメソッドで行う

	"hogefuga".Replace("hoge", "piyo")

<table>
<tr><th>書式指定子</th><th>説明</th><th>例</th><th>出力</th></tr>
<tr><td>{0}</td><td>特定の要素を表示する</td><td>'{0} {1}' -f 10, 20</td><td>10 20</td></tr>
<tr><td>{0:x}</td><td>数値を16進数で表示する(xが小文字なら出力も小文字、<br />大文字なら出力も大文字となる)</td><td>'0x{0:x}' -f 10</td><td>0xa</td></tr>
<tr><td>{0:dn}</td><td>10進数を左揃えで表示し、0でパディングする</td><td>'{0:d5}' -f 4</td><td>00004</td></tr>
<tr><td>{0:p}</td><td>数値をパーセントで表示する</td><td>'{0:p}' -f 0.543</td><td>54.30%</td></tr>
<tr><td>{0:c}</td><td>数値を通貨で表示する</td><td>'{0:c}' -f 100</td><td>\100</td></tr>
<tr><td>{0,n}</td><td>フィールド幅nで表示し、右揃えにする</td><td>'|{0,4}|' -f 20</td><td>|__20|</td></tr>
<tr><td>{0,-n}</td><td>フィールド幅nで表示し、左揃えにする</td><td>'|{0,-4}|' -f 20</td><td>|20__|</td></tr>
<tr><td>{0:hh}<br />{0:mm}<br />{0:ss}</td><td>DateTime値から時間と分と秒を表示する</td><td>'{0:hh}:{0:mm}:{0:ss}' -f (get-date)</td><td>08:24:12</td></tr>
</table>


## 応用

### 特定の文字を含むファイルのみ処理する
	Get-Get-ChildItem -Filter "*.sql" | 
	Where-Object{ (Get-Content $_) -match "^CREATE TABLE TR_"} | 
	%{ Copy-Item $_ .\作成対象\ }
