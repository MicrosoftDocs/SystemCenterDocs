---
title: Backup methods for the DPM database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5caa64ee-9163-4f9f-b7ae-257b8c15e03c
---
# Backup methods for the DPM database
As part of your DPM backup strategy, you’ll have to back up the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] database. The DPM database is named DPMDB. This database contains the DPM configuration together with data about DPM’s backups. In case of disaster, you can rebuild most of the functionality of a DPM server by using a recent backup of the database. Assuming you can restore the database, tape\- based backups are accessible, and they maintain all protection group settings and backup schedules. If the DPM storage pool disks were not affected by the outage, disk\-based backups are also usable after a rebuild. You can back up the database by using several different methods.

|Database backup method|Advantages|Disadvantages|
|--------------------------|--------------|-----------------|
|[Back up to Azure](#BKMK_Azure)|Easily configured and monitored in DPM.<br /><br />Multiple locations of the backup database files.<br /><br />Cloud storage provides a robust solution for disaster recovery.<br /><br />Very secure storage for the database.<br /><br />Supports 120 online recovery points.|Only available on DPM 2012 SP1 or later.<br /><br />Requires Azure account and additional DPM configuration. Incurs some cost for Azure storage.<br /><br />\- Requires an alternate Windows Server 2012 based system with the Azure agent to gain access to DPM backups stored in the Azure backup vault. This can’t be another DPM server.<br /><br />Not an option if the database is hosted locally and you want to enable secondary protection. A workaround would be to use a remote SQL Server to host the database.<br /><br />Some extra preparation and recovery time is incurred.|
|[Back up to the DPM storage pool](#BKMK_Pool)|Simple to configure and monitor.<br /><br />The backup is kept on the DPM storage pool disks and is easy to access locally.<br /><br />DPM scheduled backups support 512 express full backups. If you back up hourly you’ll have 21 days of full protection.|Not a good option for disaster recovery. It’s online and recovery might not work as expected if the DPM server or storage pool disk fails.<br /><br />Not an option if the database is hosted locally and you want to enable secondary protection. A workaround would be to use a remote SQL Server to host the database.<br /><br />Some preparation and special steps are required to gain access to the recovery points if the DPM service or console isn’t running or working.|
|[Back up to a secondary DPM server](#BKMK_Secondary)|Easily configured and monitored in DPM.<br /><br />DPM scheduled backups support 512 express full backups. If done hourly, this provides 21 days of short term protection. If done every 30 minutes, it provides 10 days of protection.<br /><br />The backup is kept on the secondary DPM server storage pool disks which are locally accessible.<br /><br />Provides a good disaster recovery solution if secondary DPM server is offsite.|Additional DPM server and storage are required. Both DPM servers must to be running the same DPM version and update rollups.|
|[Back up to tape](#BKMK_Tape)|Easily configured and monitored in DPM.<br /><br />DPM scheduled tape backups support retention up to 99 years.<br /><br />Tape backup can be taken offsite for disaster recovery.<br /><br />Tape backup can be restored from any other DPM server that has a tape drive\/library attached that uses the same tape media type.<br /><br />Tape can be encrypted for secure storage.|Not an option if the database is hosted locally and you want to enable secondary protection. A workaround would be to use a remote SQL Server to host the database.<br /><br />Only one tape backup per day can be scheduled.<br /><br />You need a working DPM server with a tape library to be able to read a DPM backup tape that contains the copy of the database you want to restore.<br /><br />Some preparation and special steps are required to gain access to the tape based recovery points.|
|[Back up with native SQL Server backup to a local disk](#BKMK_SQL)|Built\-in to SQL Server.<br /><br />The backup is kept on a local disk which is easily accessible.<br /><br />It can be scheduled to run as often as you like.<br /><br />Totally independent of DPM.<br /><br />You can schedule a backup file cleanup.|Not a good option for disaster recovery unless the backups are copied to a remote location.<br /><br />Requires local storage for backups which may limit retention and frequency.|
|[Back up with native SQL backup and DPM protection to a share protected by DPM](#BKMK_SQLDPM)|Easily monitored in DPM.<br /><br />Multiple locations of the backup database files.<br /><br />Easily accessible from any Windows machine on the network.<br /><br />Potentially the fastest recovery method.|Only supports 64 recovery points.<br /><br />Not a good option for site disaster recovery. DPM server or DPM storage pool disk failure may hinder recovery efforts.<br /><br />Not an option if the DPM DB is hosted locally and you want to enable secondary protection. A workaround would be to use a remote SQL Server to host the DPMDB.<br /><br />Some extra preparation is needed to get it configured and tested.<br /><br />Some extra preparation and recovery time is needed should the DPM server itself be down but DPM storage pool disks are fine.|

-   If you back up by using a DPM protection group, we recommend that you use a unique protection group for the database.

-   As a best practice, if you’re backing up to tape, make at least two copies of the backup tapes, and store each of the backup tapes in a different remote location. This added protection guards against physical damage or loss of the backup tape.

-   If the DPM SQL Server instance isn’t running on the DPM server, install the DPM protection agent on the SQL Server computer before you can protect the DPM databases on that server.

-   NOTE: For restore purposes, the DPM installation you want to restore with the DPM database must match the version of the DPM database itself.  For example, if the database you want to recover is from a DPM 2012 R2 with Update Rollup 4 installation, the DPM server must be running the same version with Update Rollup 4. This means that you might have to uninstall and reinstall DPM with a compatible version before you restore the database.  To check the database version you might have to mount it manually to a temporary database name and then run a SQL query against the database to check the last installed rollup, based on the major and minor versions. To check the DPM database version, follow these steps:

    1.  To run the query, open SQL Management Studio, and then connect to the SQL instance that’s running the DPM database.

    2.  Select the DPM database, and then start a new query.

    3.  Paste the following SQL query into the query pane and run it:

        **Select distinct MajorVersionNumber,MinorVersionNumber ,BuildNumber, FileName FROM dbo.tbl\_AM\_AgentPatch order byMajorVersionNumber,MinorVersionNumber,BuildNumber**

    If nothing is returned in the query results, or if the DPM server was upgraded from previous versions but no new update rollup was installed since then, there won’t be an entry for the major, minor for a base installation of DPM. To check the DPM versions associated with update rollups see [List of Build Numbers for System Center Data Protection Manager \(DPM\)](http://social.technet.microsoft.com/wiki/contents/articles/4058.list-of-build-numbers-for-system-center-data-protection-manager-dpm.aspx).

## <a name="BKMK_Azure"></a>Back up to Azure
You can back up the DPM database to Azure as follows:

**Before you start**

-   To recover from Azure backup you’ll need to know the DPM replica volume mount point path so that you know which recovery point contains the DPM backup. You should do this after the initial replication and you can use this script to do that. Replace **dpmsqlservername%** with the name of the SQL Server hosting the database.

    ```
    Select ag.NetbiosName as ServerName,ds.DataSourceName,vol.MountPointPath
    from tbl_IM_DataSource as ds
    join tbl_PRM_LogicalReplica as lr on ds.DataSourceId=lr.DataSourceId
    join tbl_AM_Server as ag on ds.ServerId=ag.ServerId
    join tbl_SPM_Volume as vol on lr.PhysicalReplicaId=vol.VolumeSetID
    and vol.Usage =1 
    and lr.Validity in (1,2) 
    where ds.datasourcename like '%dpmdb%'
    and servername like '%dpmsqlservername%' --netbios name of server hosting DPMDB
    ```

-   Make sure you have the passcode that was specified when the Azure Recovery Services Agent was installed and the DPM server was registered in the Azure Backup vault. You’ll need this passcode to restore the backup.

**Configure the backup**

1.  Create an Azure Backup vault.

2.  Download the Azure Backup Agent installation file and vault credentials.

3.  Install the Agent on the DPM server and use the downloaded credentials to register the server in the vault.

4.  Configure a protection group that contains the DPM database, and on the **Select Data Protection Method**page of the Create New Protection Group wizard, select to back up to Azure.

Read [Set up DPM backup to Azure](https://azure.microsoft.com/en-us/documentation/articles/backup-azure-dpm-introduction/) for more information.

**Recover the database from Azure**

The preferred method would be to use another DPM 2012 R2 server with UR7 or later versions. For more information, see the details in the following KB article:

[3065246](https://support.microsoft.com/en-us/kb/3065246) \- Update Rollup 7 for System Center 2012 R2 Data Protection Manager

Alternatively, you can use a Windows Server 2008 R2 computer \(or later\) to restore the DPM database by following these steps:

1.  On any Windows 2008R2 \/ 2012 server that has internet access, install the Windows Server Backup Feature.

2.  Sign into the Windows Azure portal, and in Recovery Services under the backup vault used for the DPM server; download the agent for Windows Server and a vault credential file.

3.  Install the Azure agent on the Windows Server performing the recovery.

4.  Launch Windows Azure Backup \- then register the server by browsing to the vault credential file you downloaded in step B\).

5.  Once registered, open a Windows Power Shell command window using Administrative privileges.

    The PowerShell commands below will detail a single recovery from a backup vault that has backups from two DPM servers. We will restore the latest DPMDB backup for **LC2\-DPMLIB2** from the backup vault.

    ```
    Windows PowerShell
    Copyright (C) 2012 Microsoft Corporation. All rights reserved.

    # get a list of servers available to recover backups for. Note: You need to supply the location and name of previously downloaded Vault Credentials file.

    PS C:\Windows\system32> $Server=Get-OBAlternateBackupServer –VaultCredentials C:\temp\DPM-Backup_day_date.vaultCredentials 
    PS C:\Windows\system32> $server    #display the list of servers
    Vault credentials validation succeeded. Below are the backup vault details.
    CertThumbprint      : 15115da73b4276e6cd8e68506aad18aa100a6543
    SubscriptionID      : ########-####-####-####-############
    ServiceResourceName : DPM-Backups
    Region              : centralus
    extensionData : System.Runtime.Serialization.ExtensionDataObject
    ServerName    : lc2-dpmlib1.Contoso.com
    ExtensionData : System.Runtime.Serialization.ExtensionDataObject
    ServerName    : lc2-dpmlib2.Contoso.com

    # Select the name of the server to recover data for.
    PS C:\Windows\system32> $name = $server[2].ServerName -Like "lc2-dpmlib2*"
    PS C:\Windows\system32> $name
    lc2-dpmlib2.Contoso.com

    # After extracting the name you need to create a server object as Get-OBrecoverableSource –Server requires a server object not just a string.
    PS C:\Windows\system32> $obj = new-object -TypeName Microsoft.Internal.CloudBackup.ObjectModel.OMCommon.CBBackupServer
    PS C:\Windows\system32> $obj.ServerName = $name
    # Get a list of sources for the DPM server using the new $obj 
    PS C:\Windows\system32> $source = Get-OBRecoverableSource -server $obj
    PS C:\Windows\system32> $source

    # Note the datasource path from the SQL Script you ran in preparation step - we want to list recovery points for that data source. In this case vol_850b95be-b942-4351-83bd-0a1815a936b2.

    FriendlyName       : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    RecoverySourceName : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    ServerName         : lc2-dpmlib2.Contoso.com

    FriendlyName       : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_79d00c30-4329-4542-b874-ada91b78f90b\
    RecoverySourceName : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_79d00c30-4329-4542-b874-ada91b78f90b\
    ServerName         : lc2-dpmlib2.Contoso.com

    # list recovery points for the first datasource [0] highlighted above.

    PS C:\Windows\system32> $item=Get-OBRecoverableItem -Source $source[0]
    PS C:\Windows\system32> $item

    # Note the date / time for the three PointInTime backups listed below.

    IsDir                : False
    ItemNameFriendly     : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    ItemNameGuid         : \\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\
    LocalMountPoint      : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    MountPointName       : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    Name                 : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    PointInTime          : 6/18/2014 1:00:13 AM
    ServerName           : lc2-dpmlib2.Contoso.com
    ItemSize             :
    ItemLastModifiedTime :

    IsDir                : False
    ItemNameFriendly     : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    ItemNameGuid         : \\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\
    LocalMountPoint      : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    MountPointName       : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    Name                 : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    PointInTime          : 6/17/2014 1:00:18 AM
    ServerName           : lc2-dpmlib2.Contoso.com
    ItemSize             :
    ItemLastModifiedTime :

    IsDir                : False
    ItemNameFriendly     : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    ItemNameGuid         : \\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\
    LocalMountPoint      : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    MountPointName       : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    Name                 : c:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\
    PointInTime          : 6/16/2014 1:01:16 AM
    ServerName           : lc2-dpmlib2.Contoso.com
    ItemSize             :
    ItemLastModifiedTime :

    # we're creating $option variable for the recovery locaton c:\temp - adjust accordingly.

    PS C:\Windows\system32> $option = new-OBRecoveryOption -Destinationpath c:\temp -Overwritetype CreateCopy

    # Here you need the same DPMPassPhrase used on the DPM Server that created the backup.

    PS C:\Windows\system32> $key = ConvertTo-Securestring "DPMPassPhrase" -Asplaintext -force

    # Start the recovery for the first backup time 6/18/2014 1:00:13 AM  from above which is $item[0].

    PS C:\Windows\system32> start-OBRecovery -recoverableItem $item[0] -EncryptionPassPhrase $key -recoveryOption $option
    Preparing storage...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Estimating size of backup items...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Transferring data...
    Data transfer completed
    Job completed.
    The recovery operation completed successfully.
    PS C:\Windows\system32>

    ```

    After a successful recovery the DPM database files will be in the location specified with the **$option** variable above.

## <a name="BKMK_Pool"></a>Back up to the DPM storage pool
With this method, you back up the DPM database as you would any other protected data source.

**Before you start:**

-   In order to recover, you’ll need to know which volume contains the backed up database. To do this, check the DPM replica volume mount point path or volume GUID after initial replication but before you need to restore.

    Use the following SQL query to retrieve the information about the volume containing the DPM database and store it in a safe place that will be accessible if disaster occurs. Replace %**dpmsqlservername**% with the name of the SQL Server hosting the DPM database.

    ```
    Select ag.NetbiosName as 
    ServerName,ds.DataSourceName,vol.MountPointPath,vol.GuidName 
    from tbl_IM_DataSource as ds
    join tbl_PRM_LogicalReplica as lr on ds.DataSourceId=lr.DataSourceId
    join tbl_AM_Server as ag on ds.ServerId=ag.ServerId
    join tbl_SPM_Volume as vol on lr.PhysicalReplicaId=vol.VolumeSetID
    and vol.Usage =1 -- Replica=1, DiffArea=2
    and lr.Validity in (1,2) 
    where ds.datasourcename like '%dpmdb%'
    and servername like '%dpmsqlservername%' --netbios name of server hosting DPMDB

    ```

-   Obtain a copy of [PsExec.exe](http://technet.microsoft.com/sysinternals/bb897553) and place it on the DPM server. This PsExec.exe file will be used as a part of the recovery process.

**Configure the backup**

1.  In DPM Administrator Console, click **Protection** on the navigation bar and click **Create protection group**in the **Actions** pane.

2.  On the **Select Protection Group Type** page, select **Servers**.

3.  On the **Select group members** page, select the DPM database. If you’re running SQL Server remotely select the remote SQL Server installed and select **DPM database**. If SQL Server is running on the DPM server expand the DPM server item and select **DPMDB**.

4.  On the **Select Data Protection Method** page, select **I want short\-term protection using disk**. Specify the short\-term protection policy options. We recommend a retention range of two weeks for DPM databases.

**Recover the database**

Assuming the DPM server itself is still operational and the storage pool is intact but the DPM service or console has problems do the follows to copy the database from the replica volume or a shadow copy.

1.  Decide the time from which you want to recover the database:

    -   If you want to copy the database from the last backup taken directly from the DPM replica volume, use mountvol.exe to assign a drive letter to the replica volume using the GUID from the SQL script output. For example: **C:\\Mountvol X: \\\\?\\Volume{d7a4fd76\-a0a8\-11e2\-8fd3\-001c23cb7375}\\**

    -   If you want to copy the database from a previous recovery point \(shadow copy\) then you need to list all the shadow copies for the replica using the volume GUID from the SQL script output. This command lists shadow copies for that volume:  **C:\\>Vssadmin list shadows \/for\=\\\\?\\Volume{d7a4fd76\-a0a8\-11e2\-8fd3\-001c23cb7375}\\**. Note the c**reation time** and the **shadow copy ID** you want to recover from. Here’s an example:

        ```
        C:\Windows\system32>vssadmin list shadows /for=\\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\
        vssadmin 1.1 - Volume Shadow Copy Service administrative command-line tool
        (C) Copyright 2001-2013 Microsoft Corp.
        Contents of shadow copy set ID: {7c67f31b-9b5b-45fc-8c9c-3688cce6bc87}
           Contained 1 shadow copies at creation time: 7/1/2014 8:00:03 PM
              Shadow Copy ID: {9f521455-dd96-4a80-8ad0-b5b1892c2f31}
                 Original Volume: (C:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\)\\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\
                 Shadow Copy Volume: \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy162
                 Originating Machine: lc2-dpmlib2.Contoso.com
                 Service Machine: lc2-dpmlib2.Contoso.com
                 Provider: 'Microsoft Software Shadow Copy provider 1.0'
                 Type: DataVolumeRollback
                 Attributes: Persistent, No auto release, No writers, Differential

        Contents of shadow copy set ID: {c23c0987-4ebe-462f-9bd4-c90ffbefc725}
           Contained 1 shadow copies at creation time: 7/2/2014 8:00:02 PM
              Shadow Copy ID: {ad959229-4f9f-43ce-8c84-014fdbf81a08}
                 Original Volume: (C:\Program Files\Microsoft DPM\DPM\Volumes\Replica\SqlServerWriter\vol_850b95be-b942-4351-83bd-0a1815a936b2\)\\?\Volume{d7a4fd76-a0a8-11e2-8fd3-001c23cb7375}\
                 Shadow Copy Volume: \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy164
                 Originating Machine: lc2-dpmlib2.Contoso.com
                 Service Machine: lc2-dpmlib2.Contoso.com
                 Provider: 'Microsoft Software Shadow Copy provider 1.0'
                 Type: DataVolumeRollback
                 Attributes: Persistent, No auto release, No writers, Differential

        ```

2.  Now use diskshadow.exe to mount the shadow copy to an unused drive letter X: using the shadow copy ID so you can copy the database files. Here’s an example:

    ```
    C:\>diskshadow.exe
    Microsoft DiskShadow version 1.0
    Copyright (C) 2013 Microsoft Corporation
    On computer:  LC2-DPMLIB2,  7/3/2014 4:31:42 PM
    DISKSHADOW> expose {ad959229-4f9f-43ce-8c84-014fdbf81a08} X:

    ```

    The shadow copy was successfully exposed as X:\\.

    ```
    DISKSHADOW> exit

    ```

    Open an administrative command prompt and run **psexec.exe \-s cmd.exe** to start a command prompt in system context so you have permissions to navigate the replica volume \(X:\) to copy out the files.

    ```
    C:\>psexec.exe -s cmd
    PsExec v1.96 - Execute processes remotely
    Copyright (C) 2001-2009 Mark Russinovich
    Sysinternals - www.sysinternals.com

    Microsoft Windows [Version 6.3.9600]
    (c) 2013 Microsoft Corporation. All rights reserved.

          C:\Windows\system32>

    ```

    Now CD to the X: drive and navigate down to the location of DPM SQL database files and copy them to a location that is easy to restore from.

    ```
    C:\Windows\system32>X:
    X:\>dir
     Volume in drive X is DPM-vol_850b95be-b942-4351-
     Volume Serial Number is 6E39-5066
     Directory of X:\

    07/01/2014  08:10 PM    <DIR>          26ee79bf-f37d-49ac-970c-cfb1d016b39c
    06/18/2014  08:00 PM                30 {26EE79BF-F37D-49AC-970C-CFB1D016B39C}checkpoint
                   1 File(s)             30 bytes
                   1 Dir(s)   8,654,036,992 bytes free

    X:\>cd 26ee79bf-f37d-49ac-970c-cfb1d016b39c
    X:\26ee79bf-f37d-49ac-970c-cfb1d016b39c>
    ...
    ..
    .
    X:\26ee79bf-f37d-49ac-970c-cfb1d016b39c\Full\C-Vol\Program Files\Microsoft DPM\DPM\DPMDB>dir
     Volume in drive E is DPM-vol_850b95be-b942-4351-
     Volume Serial Number is 6E39-5066

     Directory of X:\26ee79bf-f37d-49ac-970c-cfb1d016b39c\Full\C-Vol\Program Files\Microsoft DPM\DPM\DPMDB
    02/10/2014  11:28 AM    <DIR>          .
    02/10/2014  11:28 AM    <DIR>          ..
    06/24/2014  06:58 PM     7,171,211,264 MSDPM2012$DPMDB.mdf
    06/24/2014  06:58 PM    27,038,842,880 MSDPM2012$DPMDB_log.ldf
                   2 File(s) 34,210,054,144 bytes
                   2 Dir(s)   8,654,036,992 bytes free
    X:\26ee79bf-f37d-49ac-970c-cfb1d016b39c\Full\C-Vol\Program Files\Microsoft DPM\DPM\DPMDB>copy *.* c:\temp
    MSDPM2012$DPMDB.mdf
    MSDPM2012$DPMDB_log.ldf
     2 file(s) copied.

    ```

    After the copy is complete, exit the psexec cmd window, then run **diskshadow.exe** and unexpose the x: volume.

    ```
    C:\>Diskshadow.exe
    DISKSHADOW> unexpose X:
    Shadow copy ID {ad959229-4f9f-43ce-8c84-014fdbf81a08} is no longer exposed.%DPMDB

    ```

    You can now restore the database files by using SQL Management Studio or by running DPMSYNC –RESTOREDB. See [Recover with the DPMSync tool](#BKMK_Sync).

## <a name="BKMK_Secondary"></a>Back up to a secondary DPM server
Configure the backup

1.  On the secondary DPM server push the protection agent to the server on which the DPM database is installed – either on the primary DPM server or on a remote SQL Server. After installation the server will appear in **Unprotected server with protection agents** and should show status **OK** when refreshed.

2.  Create a new protection group. In **Select group member** choose the server hosting the DPM database. In **All SQL Servers** select the database you want to protect.

3.  In the **Select Data Protection Method** page select **I want short\-term protection** using disk or tape, and online backup if available.

4.  On the **Specify Short\-Term Goals** page select how to you want configure backups to short\-term storage. For disk storage you can have 512 express full backups as often as every 30 minutes.

5.  Finish the wizard. Protection will start after the initial recovery point is created.

**Recover the database from the secondary server**

1.  Rebuild the primary server as a DPM server if required.

2.  To restore the database, in the DPM Administrator Console on the secondary server, click **Recovery** on the navigation bar.

3.  Browse or search for the protected database. Available recovery points are indicated in bold on the calendar in the recovery points section. Select the date for the recovery point you want to recover. Recover the database to the original location.

4.  After recovering the database run the DPMSync tool. See [Recover with the DPMSync tool](#BKMK_Sync).

## <a name="BKMK_Tape"></a>Back up the database to tape
**Before you start**

You’ll need to know the barcode or tape labels of the tapes that contain a copy of the DPM database. The best way to do this is to schedule a Status Report to be mailed on the same day that the DPM database is backed up. The report will include the last backup date\/time, the tape label and the barcode so that you can locate it for recovery. Alternatively you can use this SQL script to extract the information from the current database so you can to store it separately in case of disaster.

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

**Configure the backup**

1.  In [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] Administrator Console, click **Protection** on the navigation bar and click **New** in the **Actions** pane.

2.  On the **Select group members** page, if you’re running SQL Server remotely select the remote SQL Server installed and select **DPM database**. If SQL Server is running on the DPM server expand the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server item and select **DPMDB**.

3.  On the **Select data protection method** page, select **I want short\-term protection using tape**.  Specify the short\-term protection policy options. We recommend a retention range of two weeks for [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] databases.

4.  In the **Select Library and Tape Details** page select the library you want to use for your tape backups. In **Drives allocated**, select the number of drives you want to allocate for the tape backups. In the **Copy library**section, if you want to copy data across multiple sites, select the library you want to use for the multiple backup copies.

5.  In the Tape options for long\-term protection section, do the following:

    -   Select **Check backup for data integrity**to check for data integrity between the backup copy versions.

    -   Select the **Compress data**option to enable data compression on tape, which reduces the space needed on the tape and increases the number of backup jobs that can be stored on the same tape.

    -   Select the **Encrypt data**option to encrypt the data before it is written to tape, which increases the security for archived data.

    -   Select the **Do not compress or encrypt data**option if you do not want DPM to perform data compression or encryption.

6.  Complete the Create New Protection Group Wizard with the protection options you want to use.

**Recover the database from tape**

Before you start note the following:

-   The restore process will depend on the tape hardware available and the current state of the DPM server that took the tape\-based backup. If you can’t restore the tape from the DPM server that did the backup, you’ll need to restore it from another DPM server that has the same type of tape drive so that the tape can be read. You might need to rebuild the DPM server if the only tape hardware available was the one attached to the failed DPM server.

-   If you’re using DPM tape encryption, you’ll need the same certificate used to encrypt the tape installed on the alternate DPM server.

1.  Locate the physical tape that contains the version\/date\/time of the DPM database you want to restore.

2.  Insert the backup tape into the tape drive or library and perform a detailed inventory in the DPM console \-> **Management** –>**Libraries**. Note that If the DPM server you are restoring from is a different DPM server, or it’s a new installation of DPM on the original server, the tape will be shown as imported \(not created by this DPM server\).

3.  If necessary, recatalog the imported tape.

4.  On the recovery tab, locate the database data source. If it was from an imported tape, the recovery point will be under **External DPM tapes**.

5.  Recover the database \(DPMDB\) files. You can select to **Recover to any instance of SQL Server** or to **Copy to a network folder**.

6.  After the files are restored from tape, continue with recovery steps using SQL Management Studio or DPMSYNC –RESTOREDB. For more information see [Recovery with the DPMSync tool](#BKMK_Sync).

## <a name="BKMK_SQL"></a>Back up with native SQL Server backup to a local disk
You can simply back up the DPM database to a local disk with native SQL Server backup, independent of DPM.

1.  Get an [overview](http://technet.microsoft.com/library/ms187048(v=sql.110).aspx) of SQL Server backup.

2.  [Learn more](http://technet.microsoft.com/library/jj919148(v=sql.110).aspx) about backing up SQL Server to the cloud.

## <a name="BKMK_SQLDPM"></a>Back up with native SQL Server backup to a share protected by DPM
This backup option leverages native SQL to back up the DPM database to a share, protects the share with DPM, and uses Windows VSS previous versions to facilitate the restore.

**Before you start**

1.  If the DPM database is located on a remote SQL Server, install the DPM agent on that server.

2.  On the SQL Server make a folder on a drive with enough free space to hold a single copy of a backup. For example: C:\\DPMBACKUP.

3.  Share the folder. For example share C:\\DPMBACKUP folder as DPMBACKUP.

4.  Copy and paste the OSQL command below into Notepad and save it to a file named C:\\DPMBACKUP\\bkupdb.cmd. Make sure there is no .txt extension. Modify the SQL\_Instance\_name andDPMDB\_NAME to match the instance and DPMDB name used by your DPM server.

    ```
    OSQL -E -S localhost\SQL_INSTANCE_NAME -Q "BACKUP DATABASE DPMDB_NAME TO DISK='C:\DPMBACKUP\dpmdb.bak' WITH FORMAT"

    ```

5.  Using Notepad, open the ScriptingConfig.xml file located under the ...\\DPM\\Scripting folder.

    -   On a remote SQL Server: **C:\\Program Files\\Microsoft Data Protection Manager\\DPM\\Scripting**

    -   On a DPM 2012 R2 server: **C:\\Program Files\\Microsoft System Center 2012 R2\\DPM\\DPM\\Scripting**

    -   On a DPM 2012 or 2012 with SP1 server: **C:\\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Scripting**

    -   On a DPM 2010 server, or on a DPM 2012 server upgraded from DPM 2010: **C:\\Program Files\\Microsoft DPM\\DPM\\Scripting**

6.  Modify ScriptingConfig.xml and change DataSourceName\= to be the drive letter that contains the DPMDBBACKUP folder\/share. Change the PreBackupScript entry to the full path and name of thebkupdb.cmd saved in step 5.

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

7.  Save the changes to ScriptingConfig.xml.

8.  Protect the C:\\DPMBACKUP folder or the \\\\sqlservername\\DPMBACKUP share using DPM and wait for the initial replica to be created. There should be a dpmdb.bak in the C:\\DPMBACKUPfolder as a result of the pre\-backup script running which was in turn copied to the DPM replica.

9. If you don’t enable self\-service recovery, you’ll need some additional steps to share out the DPMBACKUP folder on the replica:

    1.  \) In the DPM console > **Protection**, locate the DPMBACKUP data source and select it. In the details section, click **Click to view details** on the link to the replica path and copy the path into Notepad. Remove the source path and retain the destination path. The path should look similar to the following: **C:\\Program Files\\Microsoft System Center 2012 R2\\DPM\\DPM\\Volumes\\Replica\\File System\\vol\_c9aea05f\-31e6\-45e5\-880c\-92ce5fba0a58\\454d81a0\-0d9d\-4e07\-9617\-d49e3f2aa5de\\Full\\DPMBACKUP**.

    2.  Make a share to that path using the share name **DPMSERVERNAME\-DPMDB**. You can use the Net Share command below from an administrative command prompt.

        ```
        Net Share DPMSERVERNAME-dpmdb="C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Volumes\Replica\File System\vol_c9aea05f-31e6-45e5-880c-92ce5fba0a58\454d81a0-0d9d-4e07-9617-d49e3f2aa5de\Full\DPMBACKUP"
        ```

**Configure the backup**

You can back up the DPM database as you would any other SQL Server database using SQL Server native backup.

-   Get an [overview](http://technet.microsoft.com/library/ms187048(v=sql.110).aspx) of SQL Server backup.

-   [Learn more](http://technet.microsoft.com/library/jj919148(v=sql.110).aspx) about backing up SQL Server to the cloud.

**Recover the database**

1.  Connect to the **\\\\DPMServer\\DPMSERVERNAME\-dpmdb** share using Explorer from any Windows computer.

2.  Right\-click the dpmdb.bak file to view properties. On the **Previous Versions** tab are all the backups that you can select and copy. There is also the very last backup still located in the C:\\DPMBACKUP folder which is also easily accessible.

3.  If you need to move a SAN attached DPM storage pool disk to another server to be able to read from the replica volume, or to reinstall Windows to read locally attached disks, you’ll need to know the DPM Replica volume Mount point path or Volume GUID beforehand so you know what volume holds the database backup. You can use the SQL script below to extract that information any time after initial protection but before the need to restore. Replace the %dpmsqlservername% with the name of the SQL Server hosting the database.

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

    1.  You have the volume GUID, so should that volume need to be mounted on another Windows server or after a DPM server rebuild, use mountvol.exe to assign it a drive letter using the volume GUID from the SQL script output: **C:\\Mountvol X: \\\\?\\Volume{d7a4fd76\-a0a8\-11e2\-8fd3\-001c23cb7375}\\**.

    2.  Reshare the DPMBACKUP folder on the replica volume using the drive letter and portion of the replica path representing the folder structure.

        ```
        net share SERVERNAME-DPMDB="X:\454d81a0-0d9d-4e07-9617-d49e3f2aa5de\Full\DPMBACKUP"

        ```

    3.  Connect to the \\\\SERVERNAME\\DPMSERVERNAME\-dpmdb share using Explorer from any Windows computer

    4.  Right\-click the dpmdb.bak file to view the Properties. On the **Previous Versions** tab are all the backups that you can select and copy.

## <a name="BKMK_Sync"></a>Recover with the DPMSync tool
You can use the DPMSync tool to restore backups taken by DPM, DPMBackup.exe, and native SQL Server backup. It can restore backups with the .bak extension, or restore SQL Server database files with the .mdf and .ldf extensions. Note additions to this tool:

-   From DPM 2012 support was added for multiple DPM servers to share one instance of SQL Server for the DPM database.

-   From DPM 2012 R2 support for a SQL Server cluster used as the DPM database.

The result of these changes is an increase for required parameters when you run DPMSync.exe to restore a DPM 2012 database.

The DPMSync.exe utility is installed by default in the DPM installation path inside the **bin** folder. However, this should already be added to the %path%system variable and can run from any administrative command prompt.

Run the tool as needed.

**Scenarios**

**Restore the database on a remote SQL Server**

*Note that when using the default instance specify **\(local\)** or a period \(**.**\) for the instance name.*

```
C:\Program Files\Microsoft Data Protection Manager\DPM2012\SQLPrep>dpmsync -restoredb -dbloc c:\temp\dpmdb_dpm03.bak -instancename DPMSQLDB -dpmdbname dpmdb_dpm03
DpmSync 2.0 - DPM database synchronization command-line tool
Copyright (c) 2012 Microsoft Corporation. All rights reserved.
Restoring DPM Database completed.

```

**Restore the database on the local DPM server using the .mdf file**

```
C:\>dpmsync -restoredb -dbloc E:\MSDPM2012$DPMDB.mdf -instancename dpmserver\msdpm2012 -dpmdbname dpmdb
DpmSync 2.0 - DPM database synchronization command-line tool
Copyright (c) 2013 Microsoft Corporation. All rights reserved.
Copying file from 'e:\msdpm2012$dpmdb.mdf' to 'C:\Program Files\Microsoft System Center 2012\DPM\DPM\DPMDB\MSDPM2012$DPMDB.mdf.recovered'
Copying file from 'e:\msdpm2012$dpmdb_log.ldf' to 'C:\Program Files\Microsoft System Center 2012\DPM\DPM\DPMDB\MSDPM2012$DPMDB_log.ldf.recovered'
Files copied successfully.
Database detached successfully.
Renamed file 'MSDPM2012$DPMDB.mdf.recovered' to 'MSDPM2012$DPMDB.mdf'
Renamed file 'MSDPM2012$DPMDB_log.ldf.recovered' to 'MSDPM2012$DPMDB_log.ldf'
Database attached successfully.
Restoring DPM Database completed.

```

*If you restore .mdf files to a database that isn’t named DPMDB see Microsoft article [2968666](http://support.microsoft.com/kb/2968666)*.

Anytime a database is restored from a backup you need to run the DpmSync \-Sync command to reconcile backup job run times, DPM storage pool usage and other configuration settings that might have changed since the restored database backup time. The DPMSYNC –SYNC command must be run on the DPM server where it has access to the storage pool and snapshots. A consistency check will be required on all data sources before normal protection can be resumed.

On the DPM server run:

```
C:\>dpmsync –sync
DpmSync 2.0 - DPM database synchronization command-line tool
Copyright (c) 2013 Microsoft Corporation. All rights reserved.
Note: The DPM role configuration of this server will also be rolled back during this operation.
DPM Synchronization completed.
Your tape library status may have changed.
Recommendation: Go to the Library tab in the Management Task Area of the DPM Administration Console and choose the Inventory Library action.

```


