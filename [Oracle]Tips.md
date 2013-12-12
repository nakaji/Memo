#Oracleメモ

##エクスポート、インポート

###ディレクトリオブジェクトの一覧を取得する
	SELECT * FROM ALL_DIRECTORIES

###ディレクトリオブジェクトの作成
	create directory EXP_DIR as 'D:\Exp';

###エクスポート
	expdp system/*** DUMPFILE=expdat.dmp DIRECTORY=EXP_DIR SCHEMAS=SCOTT

###インポート
	impdp system/*** DUMPFILE=expdat.dmp DIRECTORY=EXP_DIR REMAP_SCHEMA=SCOTT:TIGER

##その他

###INVALIDなオブジェクトを再コンパイル
	CALL UTL_RECOMP.RECOMP_SERIAL('SUB01');

###INVALIDなオブジェクトを表示
	SELECT owner, object_type, status, object_name
	FROM all_objects
	WHERE status = 'INVALID'
	AND owner='SUB01';

