#[SQLServer]障害発生時点までの復旧

##バックアップ
	ALTER DATABASE AdventureWorks SET RECOVERY FULL;
	BACKUP DATABASE AdventureWorks TO DISK = 'D:\AdventureWorks_Data.bck';
	BACKUP LOG AdventureWorks TO DISK = 'D:\AdventureWorks_Log.bck';


##リストア
	/* Example of restoring a to the point of failure */
	-- Step 1: Create a tail-log backup by using WITH NORECOVERY.
	BACKUP LOG AdventureWorks
	   TO DISK = 'D:\AdventureWorks_Log_tail.bck'
	   WITH NO_TRUNCATE;
	GO
	-- Step 2: Restore the full database backup.
	RESTORE DATABASE AdventureWorks
	   FROM DISK = 'D:\AdventureWorks_Data.bck'
	   WITH NORECOVERY;
	GO
	-- Step 3: Restore the first transaction log backup.
	RESTORE LOG AdventureWorks
	   FROM DISK = 'D:\AdventureWorks_Log.bck'
	   WITH NORECOVERY;
	GO
	-- Step 4: Restore the tail-log backup.
	RESTORE LOG AdventureWorks
	   FROM  DISK = 'D:\AdventureWorks_Log_tail.bck'
	   WITH NORECOVERY;
	GO
	-- Step 5: Recover the database.
	RESTORE DATABASE AdventureWorks
	   WITH RECOVERY;
	GO
