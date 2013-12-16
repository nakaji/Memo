#Oracleメモ

##エクスポート、インポート
1. [Oracle Data Pumpの概要](http://otndnld.oracle.co.jp/document/products/oracle10g/102/doc_cd/server.102/B19211-01/dp_overview.html)
1. [Data Pump Export](http://otndnld.oracle.co.jp/document/products/oracle10g/102/doc_cd/server.102/B19211-01/dp_export.html)
1. [Data Pump Import](http://otndnld.oracle.co.jp/document/products/oracle10g/102/doc_cd/server.102/B19211-01/dp_import.html)

###ディレクトリオブジェクトの一覧を取得する
	SELECT * FROM ALL_DIRECTORIES

###ディレクトリオブジェクトの作成
	create directory EXP_DIR as 'D:\Exp';

###エクスポート
	expdp system/*** DUMPFILE=expdat.dmp DIRECTORY=EXP_DIR SCHEMAS=SCOTT

###インポート
	impdp system/*** DUMPFILE=expdat.dmp DIRECTORY=EXP_DIR REMAP_SCHEMA=SCOTT:TIGER

> TABLE_EXISTS_ACTION={SKIP | APPEND | TRUNCATE | REPLACE}

##SEQUENCE

###現在の値を取得する
	select sequence_name, last_number from user_sequences order by sequence_name;
	select SEQURIDENNO.CURRVAL from dual;

##その他

###INVALIDなオブジェクトを再コンパイル
	CALL UTL_RECOMP.RECOMP_SERIAL('SUB01');

###INVALIDなオブジェクトを表示
	SELECT owner, object_type, status, object_name
	FROM all_objects
	WHERE status = 'INVALID'
	AND owner='SUB01';

