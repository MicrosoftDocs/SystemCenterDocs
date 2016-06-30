exe and unexpose the X: volume.

5.  Now you can restore the database files by using SQL Management Studio or by running DPMSYNC-RESTOREDB.

### Back up the database to a secondary server

1.  On the secondary DPM server push the protection agent to the server on which the DPM database is installed - either on the primary DPM server or on a remote SQL Server. After installation the server will appear in **Unprotected server with protection agents** and should show status OK when refreshed.

2.  Create a new protection group. In **Select group member** choose the server hosting the DPM database. In **All SQL Servers** select the database you want to protect.
    In the **Select Data Protection Method** page select to use short-term protection to disk and online if required. On the **Specify Short-Term Goals** page select how to you want configure backups to short-term storage. For disk storage you can have 512 express full backups as often as every 30 minutes.
    Finish the wizard. Protection will start after the initial recovery point is created

#### Recover the database

1.  Rebuild the primary server as a DPM server if required.

2.  To restore the database, in the DPM console on the secondary server, click **Recovery** and locate the protected database.

3.  Select the date for the recovery point you want to recover. Recover the database to the original location.
    After recovering the database run the DPMSync tool.

## Back up the database to tape
You'll need to know the barcode or tape labels of the tapes that contain a copy of the DPM database. The best way to do this is to schedule a Status Report to be mailed on the same day that the DPM database is backed up. The report will include the last backup date/time, the tape label and the barcode so that you can locate it for recovery. Alternatively you can use this SQL script to extract the information from the current database so you can to store it separately in case of disaster.

```
Select Path,ro.FileSpec,media.Label,media.BarcodeValue,pd.CreationDate,
pd.ExpiryDate,pd.LifeStatus as "1=valid, 2=expired"
from dbo.tbl_MM_MediaMap mm
join dbo.tbl_MM_PhysicalDataset pd on pd.datasetid = mm.datasetid
join dbo.tbl_MM_Media media on media.MediaId = mm.MediaId
join dbo.tbl_RM_RecoverableObjectFileSpec ro on ro.DatasetId = mm.DatasetId
where ro.filespec like '%DPMDB%'
order by CreationDate desc
```

1.  Create a protection group and on the **Select Group Members** page select the SQL Server (if it's running locally select DPMDB under the DPM server).

2.  Select to do long-term protection with tape and specify the tape details on the **Select Library and Tape Details**.

### Recover the database

-   The restore process will depend on the tape hardware available and the current state of the DPM server that took the tape-based backup. If you can't restore the tape from the DPM server that did the backup, you'll need to restore it from another DPM server that has the same type of tape drive so that the tape can be read. You might need to rebuild the DPM server if the only tape hardware available was the one attached to the failed DPM server.

-   If you're using DPM tape encryption, you'll need the same certificate used to encrypt the tape installed on the alternate DPM server.

To recover:

1.  Locate the physical tape that contains the version/date/time of the DPM database you want to restore.

2.  Insert the backup tape into the tape drive or library and perform a detailed inventory in the DPM console -> Management ->Libraries. Note that If the DPM server you are restoring from is a different DPM server, or it's a new installation of DPM on the original server, the tape will be shown as imported (not created by this DPM server).

3.  If necessary, recatalog the imported tape.

4.  On the **Recovery** tab, locate the database data source. If it was from an imported tape, the recovery point will be under **External DPM tapes**.

5.  Recover the database (DPMDB) files. You can select to Recover to any instance of SQL Server or to Copy to a network folder.
    After the files are restored from tape, continue with recovery steps using SQL Management Studio or DPMSYNC -RESTOREDB.

## Back up with native SQL Server backup to a local disk
You can simply back up the DPM database to a local disk with native SQL Server backup, independent of DPM.

1.  Get an [overview](http://technet.microsoft.com/library/ms187048(v=sql.110).aspx) of SQL Server backup.

2.  [Learn more](http://technet.microsoft.com/library/jj919148(v=sql.110).aspx) about backing up SQL Server to the cloud.

## Back up with native SQL Server backup to a share protected by DPM
This backup option leverages native SQL to back up the DPM database to a share, protects the share with DPM, and uses Windows VSS previous versions to facilitate the restore.

**Before you start**

1.  If the DPM database is located on a remote SQL Server, install the DPM agent on that server.

2.  On the SQL Server make a folder on a drive with enough free space to hold a single copy of a backup. For example: C:\DPMBACKUP.

3.  Share the folder. For example share C:\DPMBACKUP folder as DPMBACKUP.

4.  Copy and paste the OSQL command below into Notepad and save it to a file named C:\DPMBACKUP\bkupdb.cmd. Make sure there is no .txt extension. Modify the SQL_Instance_name andDPMDB_NAME to match the instance and DPMDB name used by your DPM server.

    ```
    OSQL -E -S localhost\SQL_INSTANCE_NAME -Q "BACKUP DATABASE DPMDB_NAME TO DISK='C:\DPMBACKUP\dpmdb.bak' WITH FORMAT"

    ```

5.  Using Notepad, open the ScriptingConfig.xml file located under the ...\DPM\Scripting folder.

    -   On a remote SQL Server: **C:\Program Files\Microsoft Data Protection Manager\DPM\Scripting**

    -   On a DPM 2012 R2 server: **C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Scripting**

    -   On a DPM 2012 or 2012 with SP1 server: **C:\Program Files\Microsoft System Center 2012\DPM\DPM\Scripting**

    -   On a DPM 2010 server, or on a DPM 2012 server upgraded from DPM 2010: **C:\Program Files\Microsoft DPM\DPM\Scripting**

6.  Modify ScriptingConfig.xml and change DataSourceName= to be the drive letter that contains the DPMDBBACKUP folder/share. Change the PreBackupScript entry to the full path and name of thebkupdb.cmd saved in step 5.

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <ScriptConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" 
    xmlns="http://schemas.microsoft.com/2003/dls/ScriptingConfig.xsd">
    <DatasourceScriptConfig DataSourceName="C:">
    <PreBackupScript>C:\DPMDBBACKUP\bkupdb.cmd</PreBackupScript>
    <TimeOut>120</TimeOut>
    </DatasourceScriptConfig>
    </ScriptConfiguration>
    ```

7.  Save the changes to ScriptingConfig.xml.

8.  Protect the C:\DPMBACKUP folder or the \\\sqlservername\DPMBACKUP share using DPM and wait for the initial replica to be created. There should be a dpmdb.bak in the C:\DPMBACKUPfolder as a result of the pre-backup script running which was in turn copied to the DPM replica.

9. If you don't enable self-service recovery, you'll need some additional steps to share out the DPMBACKUP folder on the replica:

    1.  ) In the DPM console > **Protection**, locate the DPMBACKUP data source and select it. In the details section, click **Click to view details** on the link to the replica path and copy the path into Notepad. Remove the source path and retain the destination path. The path should look similar to the following: **C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Volumes\Replica\File System\vol_c9aea05f-31e6-45e5-880c-92ce5fba0a58\454d81a0-0d9d-4e07-9617-d49e3f2aa5de\Full\DPMBACKUP**.

    2.  Make a share to that path using the share name **DPMSERVERNAME-DPMDB**. You can use the Net Share command below from an administrative command prompt.

        ```
        Net Share DPMSERVERNAME-dpmdb="C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Volumes\Replica\File System\vol_c9aea05f-31e6-45e5-880c-92ce5fba0a58\454d81a0-0d9d-4e07-9617-d49e3f2aa5de\Full\DPMBACKUP"
        ```

**Configure the backup**

You can back up the DPM database as you would any other SQL Server database using SQL Server native backup.

-   Get an [overview](http://technet.microsoft.com/library/ms187048(v=sql.110).aspx) of SQL Server backup.

-   [Learn more](http://technet.microsoft.com/library/jj919148(v=sql.110).aspx) about backing up SQL Server to the cloud.

**Recover the database**

1.  Connect to the **\\\DPMServer\DPMSERVERNAME-dpmdb** share using Explorer from any Windows computer.

2.  Right-click the dpmdb.bak file to view properties. On the **Previous Versions** tab are all the backups that you can select and copy. There is also the very last backup still located in the C:\DPMBACKUP folder which is also easily accessible.

3.  If you need to move a SAN attached DPM storage pool disk to another server to be able to read from the replica volume, or to reinstall Windows to read locally attached disks, you'll need to know the DPM Replica volume Mount point path or Volume GUID beforehand so you know what volume holds the database backup. You can use the SQL script below to extract that information any time after initial protection but before the need to restore. Replace the %dpmsqlservername% with the name of the SQL Server hosting the database.

    ```
    Select ag.NetbiosName as 
    ServerName,ds.DataSourceName,vol.MountPointPath,vol.GuidName 
    from tbl_IM_DataSource as ds
    join tbl_PRM_LogicalReplica as lr on ds.DataSourceId=lr.DataSourceId
    join tbl_AM_Server as ag on ds.ServerId=ag.ServerId
    join tbl_SPM_Volume as vol on lr.PhysicalReplicaId=vol.VolumeSetID
    and vol.Usage =1 
    and lr.Validity in (1,2) 
    where ds.datasourcename like '%C:\%' -- volume drive letter for DPMBACKUP
    and servername like '%dpmsqlservername%' --netbios name of server hosting DPMDB

    ```

4.  If you need to recover after moving DPM storage pool disks or a DPM server rebuild:

    1.  You have the volume GUID, so should that volume need to be mounted on another Windows server or after a DPM server rebuild, use mountvol.exe to assign it a drive letter using the volume GUID from the SQL script output: **C:\Mountvol X: \\\\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\\**.

    2.  Reshare the DPMBACKUP folder on the replica volume using the drive letter and portion of the replica path representing the folder structure.

        ```
        net share SERVERNAME-DPMDB="X:\454d81a0-0d9d-4e07-9617-d49e3f2aa5de\Full\DPMBACKUP"

        ```

    3.  Connect to the \\\SERVERNAME\DPMSERVERNAME-dpmdb share using Explorer from any Windows computer

    4.  Right-click the dpmdb.bak file to view the Properties. On the **Previous Versions** tab are all the backups that you can select and copy.

