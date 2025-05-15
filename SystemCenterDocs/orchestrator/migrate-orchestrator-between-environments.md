---
title: Migrate Orchestrator between environments
description: Describes how you can automatically move Orchestrator between environments.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: intro-migration, UpdateFrequency3, engagement-fy24
---

# Migrate Orchestrator between environments

::: moniker range="<=sc-orch-2022"

This article describes how to move Orchestrator between environments, such as moving to a new SQL Server 2008 R2 or moving some components of Orchestrator.

::: moniker-end 

::: moniker range="sc-orch-2025"

This article describes how to move Orchestrator between environments, such as moving to a new SQL Server 2022 or moving some components of Orchestrator.

::: moniker-end 

The following processes and scripts enable you to easily move between environments. They're based on a full migration of all Orchestrator components to a new SQL Server machine, with a restored Orchestrator database.  

The following steps are required to enable an automatic migration of Orchestrator to a new environment:  

1. Back up SQL Server service master key in environment A  

2. Back up the Orchestrator database in environment A  

3. Deploy SQL Server in environment B  

4. Restore the SQL Server service master key in environment B  

5. Restore Orchestrator database in environment B  

6. Deploy Orchestrator components in environment B  

> [!NOTE]  
> For more information, see how to use [sqlcmd utility](https://go.microsoft.com/fwlink/?LinkId=246817).

> [!NOTE]  
> It's recommended to enable SQL Broker on the Orchestrator Database in order for internal maintenance tasks to execute automatically.  

## Check/enable SQL Broker

Check if you need to enable SQL Broker by running the following query against the Orchestrator SQL Instance:

```sql
Select Name, is_broker_enabled, Compatibility_Level from sys.databases Where name = 'Orchestrator'
```

If you notice your Orchestrator database broker is disabled (0), you'll need to enable SQL Broker with the following steps:
1.  Stop all Orchestrator related services on all Management Servers/Runbook Servers:\
    Orchestrator Management Service (`omanagement`)\
    Orchestrator Remoting Service (`oremoting`)\
    Orchestrator Runbook Server Monitor (`omonitor`)\
    Orchestrator Runbook Service (`orunbook`)
    ```powershell
    (Get-Service).Where{$_.Name -match "^omanagement|^oremoting|^omonitor|^orunbook"} | Stop-Service -Confirm:$false
    ```
2.  Run the following query against the Orchestrator SQL Instance:
    ```sql
    ALTER DATABASE Orchestrator SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    GO
    ALTER DATABASE Orchestrator SET ENABLE_BROKER
    GO
    ALTER DATABASE Orchestrator SET MULTI_USER
    GO
    ```
3.  Start all Orchestrator related services on all Management Servers/Runbook Servers:
    ```powershell
    (Get-Service).Where{$_.Name -match "^omanagement|^oremoting|^omonitor|^orunbook"} | Start-Service
    ```

## Back up SQL Server service master key in environment A

Back up the SQL Server service master key.

Create a batch script with the following command:  

```powershell
Sqlcmd -Q "BACKUP SERVICE MASTER KEY TO FILE ='C:\BACKUP\MASTER_KEY.BAK' ENCRYPTION BY PASSWORD = 'password'"  

```  

Where 'password' is the password that will be used to protect the service master key in the file that is created. If the password is lost, the service master key can't be recovered from the file.  

## Back up the Orchestrator database in environment A

Back up the entire Orchestrator database. You can perform the backup when the system is running; however, it's best to perform the backup when all runbook authors have checked in any pending changes to their runbooks. Pending changes are cached on the Runbook Designer and aren't backed up with a database backup.  

1.  In SQL Server Management, right-click the Orchestrator database, select **Tasks**, and then select **Back up**.  

2.  Configure the backup settings as required in your organization.  

3.  Select **Script**, and then select **Script Action to New Query Window**.  

4.  Select **Execute** to test the backup script.  

5.  Create a batch file with this script. Your batch file will be similar to the following:  

    ```powershell
    Sqlcmd -Q "BACKUP DATABASE Orchestrator TO DISK=N'C:\BACKUP\OrchestratorDB.bak'"  
    ```  

## Deploy SQL Server in environment B

Deploy SQL Server to environment B.

## Restore the SQL Server service master key in environment B

Restore the Microsoft SQL Server service master key to enable decryption of Orchestrator data on the new SQL server.  

Create a batch script with the command:  

>[!NOTE]
> If you intend to use\migrate the Orchestrator database in a **SQL Always ON** instance, you'll be prompted for the database encryption key password.

```powershell
Sqlcmd -Q "RESTORE SERVICE MASTER KEY FROM FILE = 'C:\BACKUP\MASTER_KEY.BAK' DECRYPTION BY PASSWORD = 'password';"  

```  

## Restore the Orchestrator database in environment B

Use the following steps to create a batch script to run on the new SQL Server computer to restore the Orchestrator database.  

1.  In SQL Server Management, right-click the Orchestrator database, select **Tasks**, and then select **Restore**.  

2.  Configure the restore settings as required in your organization.  

3.  Select **Script**, and then select **Script Action to New Query Window**.  

4.  Select **Execute** to test the restore script.  

5.  Create a batch file with this script. Your batch file will be similar to the following:  

    ```powershell
    Sqlcmd -Q "RESTORE DATABASE [Orchestrator] FROM  DISK = N'C:\BACKUP\OrchestratorDB.bak'WITH  FILE = 1,  NOUNLOAD,  STATS = 10"  

    ```  

    >[!NOTE]
    > Orchestrator database is encrypted; you need the encryption key password to add the database to an  SQL *Always ON* setup. Use the following `T-SQL` query to change the password and use the new password in the SQL **Always ON Availability** wizard while adding the database to *Always ON* setup:
    >
    >
    >**Use Orchestrator ALTER MASTER KEY**
    >
    >**REGENERATE WITH ENCRYPTION BY PASSWORD = 'password';**
    >
    >**GO**

## Deploy Orchestrator components in environment B  

Deploy Orchestrator components \(management server, Web features, runbook servers, and Runbook Designers\) using the silent install commands of Orchestrator setup. For more information on deploying Orchestrator using the command line, see [Install with the Orchestrator Command Line Install Tool](~/orchestrator/install.md).  

::: moniker range="<=sc-orch-2019"
The following example installs all of Orchestrator on a computer running SQL Server 2008 R2 and .NET Framework&nbsp;4:  
::: moniker-end

::: moniker range=">=sc-orch-2022"
The following example installs Orchestrator on a computer running SQL Server:  
::: moniker-end

::: moniker range="sc-orch-2025"

>[!NOTE]
>Review guidelines about [Secure connection to SQL server)](/SystemCenterDocs/orchestrator/install.md#secure-connection-to-sql-server).

::: moniker-end

```powershell
%systemdrive%\sco\setup\setup.exe /Silent `
    /ServiceUserName:%computername%\administrator `
    /ServicePassword:password `
    /Components:All `
    /DbServer:%computername%  /DbPort:1433 /DbNameNew:OrchestratorSysPrep `
    /WebConsolePort:82 /WebServicePublicUrl:"http://localhost:81" `
    /WebServicePort:81 /WebConsolePublicUrl:"http://localhost:82" `
    /OrchestratorRemote `
    /UseMicrosoftUpdate:1 /SendCEIPReports:1 /EnableErrorReporting:always
```  

## Sample migration scripts and commands

**Back up SQL Server master service key sample**  

```powershell
Sqlcmd -Q "BACKUP SERVICE MASTER KEY TO FILE ='C:\BACKUP\MASTER_KEY.BAK' ENCRYPTION BY PASSWORD = 'password'"  

```  

**Back up Orchestrator database sample**  

```powershell
Sqlcmd -Q "BACKUP DATABASE Orchestrator TO DISK=N'C:\BACKUP\OrchestratorDB.bak'"  
```  

**Restore SQL Server master service key sample**  

```powershell
Sqlcmd -Q "RESTORE SERVICE MASTER KEY FROM FILE = 'c:\temp_backups\keys\service_master_key' DECRYPTION BY PASSWORD = 'password'"  
```  

**Restore Orchestrator database sample**  

```powershell
Sqlcmd -Q "RESTORE DATABASE [Orchestrator] FROM  DISK = N'C:\BACKUP\OrchestratorDB.bak'WITH  FILE = 1,  NOUNLOAD,  STATS = 10"  
```  

**Install Orchestrator from batch file sample**  

```powershell
%systemdrive%\sco\setup\setup.exe /Silent `
    /ServiceUserName:%computername%\administrator `
    /ServicePassword:password `
    /Components:All `
    /DbServer:%computername%  /DbPort:1433 /DbNameNew:OrchestratorSysPrep `
    /WebConsolePort:82 /WebServicePublicUrl:"http://localhost:81" `
    /WebServicePort:81 /WebConsolePublicUrl:"http://localhost:82" `
    /OrchestratorRemote `
    /UseMicrosoftUpdate:1 /SendCEIPReports:1 /EnableErrorReporting:always  
```
