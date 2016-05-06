---
title: Migrate Orchestrator Between Environments
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2cde140-80eb-4f59-b83e-449c782a03be
---
# Migrate Orchestrator Between Environments
This topic describes how to automatically move Orchestrator between environments. This could be useful when you want to just move to a new SQL Server 2008 R2 or if you want to move some or all of the components of Orchestrator.

The following processes and scripts enable you to easily move between environments. They are based on a full migration of all System Center 2012 \- Orchestrator components to a new SQL Server 2008 R2 with a restored Orchestrator database.

The following steps are required to enable an automatic migration of Orchestrator to a new environment:

1.  Backup SQL Server service master key in environment A

2.  Backup the Orchestrator database in environment A

3.  Deploy SQL Server 2008 R2 in environment B

4.  Restore SQL Server service master key in environment B

5.  Restore Orchestrator database in environment B

6.  Deploy Orchestrator components in environment B

> [!NOTE]
> See [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=246817](http://go.microsoft.com/fwlink/?LinkId=246817) for information on using the Sqlcmd utility.

## <a name="SCO_Migrate1"></a>Back up SQL Server service master key in environment A
Back up the SQL Server 2008 R2 service master key using the following procedure as described in [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=243093](http://go.microsoft.com/fwlink/?LinkID=243093).  This is a one\-time operation.

Create a batch script with the following command:

```
Sqlcmd –Q "BACKUP SERVICE MASTER KEY TO FILE ='C:\BACKUP\MASTER_KEY.BAK' ENCRYPTION BY PASSWORD = 'password'"

```

Where ‘password’ is the password that will be used to protect the service master key in the file that is created. If the password is lost, the service master key cannot be recovered from the file.

## <a name="SCO_Migrate2"></a>Back up the Orchestrator database in environment A
Back up the entire Orchestrator database.  You can perform the backup when the system is running; however it is best to perform the backup when all runbook authors have checked in any pending changes to their runbooks. Pending changes are cached on the Runbook Designer and are not backed up with a database backup.

#### To back up the Orchestrator database

1.  In SQL Server Management, right\-click the Orchestrator database, click **Tasks**, and then click **Back up**.

2.  Configure the backup settings as required in your organization.

3.  Click **Script**, and then click **Script Action to New Query Window**.

4.  Click **Execute** to test the backup script.

5.  Create a batch file with this script. Your batch file will be similar to the following:

    ```
    Sqlcmd –Q "BACKUP DATABASE Orchestrator TO DISK=N'C:\BACKUP\OrchestratorDB.bak'"
    ```

## <a name="SCO_Migrate3"></a>Deploy SQL Server 2008 R2 in environment B
Deploy SQL Server to environment B. See [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=246815](http://go.microsoft.com/fwlink/?LinkID=246815) for information about creating a Sysprep image of SQL Server 2008 R2.

## <a name="SCO_Migrate4"></a>Restore the SQL Server service master key in environment B
Restore the Microsoft SQL Sevver 2008 R2 service master key by using the procedure described at [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=243093](http://go.microsoft.com/fwlink/?LinkID=243093).  This will enable decryption of Orchestrator data on the new SQL server.

Create a batch script with the following command:

```
Sqlcmd –Q "RESTORE SERVICE MASTER KEY FROM FILE = 'C:\BACKUP\MASTER_KEY.BAK' DECRYPTION BY PASSWORD = 'password';"

```

## <a name="SCO_Migrate5"></a>Restore the Orchestrator database in environment B
Use the following steps to create a batch script to run on the new SQL Server computer to restore the Orchestrator database.

#### To create the batch file

1.  In SQL Server Management, right\-click the Orchestrator database, click **Tasks**, and then click **Restore**.

2.  Configure the restore settings as required in your organization.

3.  Click **Script**, and then click **Script Action to New Query Window**.

4.  Click **Execute** to test the restore script.

5.  Create a batch file with this script. Your batch file will be similar to the following:

    ```
    Sqlcmd –Q "RESTORE DATABASE [Orchestrator] FROM  DISK = N'C:\BACKUP\OrchestratorDB.bak'WITH  FILE = 1,  NOUNLOAD,  STATS = 10"

    ```

## <a name="SCO_Migrate6"></a>Deploy Orchestrator components in environment B
Deploy Orchestrator components \(management server, Web features, runbook servers, and Runbook Designers\) using the silent install commands of Orchestrator setup. See [Install with the Orchestrator Command Line Install Tool](Install-with-the-Orchestrator-Command-Line-Install-Tool.md) for more information on deploying Orchestrator through the command line.

The following example installs all of Orchestrator on a computer with SQL Server 2008 R2 and .NET Framework 4:

```
%systemdrive%\sco\setup\setup.exe /Silent /ServiceUserName:%computername%\administrator /ServicePassword:password /Components:All /DbServer:%computername%  /DbPort:1433 /DbNameNew:OrchestratorSysPrep /WebConsolePort:82 /WebServicePort:81 /OrchestratorRemote /UseMicrosoftUpdate:1 /SendCEIPReports:1 /EnableErrorReporting:always

```

## Sample migration scripts and commands
**Backup SQL Server master service key sample**

```
Sqlcmd –Q "BACKUP SERVICE MASTER KEY TO FILE ='C:\BACKUP\MASTER_KEY.BAK' ENCRYPTION BY PASSWORD = 'password'"

```

**Backup Orchestrator database sample**

```
Sqlcmd –Q "BACKUP DATABASE Orchestrator TO DISK=N'C:\BACKUP\OrchestratorDB.bak'"
```

**Restore SQL Server master service key sample**

```
Sqlcmd –Q "RESTORE SERVICE MASTER KEY FROM FILE = 'c:\temp_backups\keys\service_master_key' DECRYPTION BY PASSWORD = 'password'"
```

**Restore Orchestrator database sample**

```
Sqlcmd –Q "RESTORE DATABASE [Orchestrator] FROM  DISK = N'C:\BACKUP\OrchestratorDB.bak'WITH  FILE = 1,  NOUNLOAD,  STATS = 10"
```

**Install Orchestrator from batch file sample**

```
%systemdrive%\sco\setup\setup.exe /Silent /ServiceUserName:%computername%\administrator /ServicePassword:password /Components:All /DbServer:%computername%  /DbPort:1433 /DbNameNew:OrchestratorSysPrep /WebConsolePort:82 /WebServicePort:81 /OrchestratorRemote /UseMicrosoftUpdate:1 /SendCEIPReports:1 /EnableErrorReporting:always

```


