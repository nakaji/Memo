##ダウンロード
https://github.com/pester/Pester

##モジュールのインポート
	Import-Module Pester\Pester.psm1

##テンプレートの作成
	New-Fixture .\scripts Sample
scripts配下にSample.ps1,Sample.Tests.ps1が生成される。

##例
	$here = Split-Path -Parent $MyInvocation.MyCommand.Path
	$sut = (Split-Path -Leaf $MyInvocation.MyCommand.Path).Replace(".Tests.", ".")
	. "$here\$sut"
	
	Describe "Sample" {
	
	    It "Be" {
	        "hoge" | Should Be "hoge"
	    }
	
	    It "Not Be" {
	        "hoge" | Should Not Be "fuga"
	    }
	
	    It "Exist" {
	       Get-ChildItem | Should Exist
	    }
	
	    It "Contain" {
	       "Sample.Tests.ps1"| Should Contain "hoge"
	    }
	
	    It "BeNullOrEmpty" {
	        $null | Should BeNullOrEmpty
	        "" | Should BeNullOrEmpty
	    }
	    
	    It "Match" {
	        "hoge" | Should Match "[Hh]oge"
	        "Hoge" | Should Match "[Hh]oge"
	    }
	
	    It "Throw" {
	        {throw "error message"} | Should Throw "error message"
	    }
	}
	
##Setup
	Describe "Setup" {
	    Context "Setup" {
	        Setup -File "hoge.txt" "copntent"
	        It "Contain" {
	            "$TestDrive\hoge.txt" | Should Contain "copntent"
	       }
	    }
	}
$TestDrive（$env:TEMP配下のpesterディレクトリ）にファイル等を作成する。
テストが終われば$TestDriveはディレクトリごと削除される。
