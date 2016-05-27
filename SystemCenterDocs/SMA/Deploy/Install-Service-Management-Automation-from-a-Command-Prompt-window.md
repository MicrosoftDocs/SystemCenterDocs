---
title: Install Service Management Automation from a Command Prompt window
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9849ebcc-519a-4dd5-86c1-e947121c2a6d
---
# Install Service Management Automation from a Command Prompt window
You can install the features of [!INCLUDE[sma_1](../../includes/sma_1_md.md)] by using commands in the Command Prompt window to guide the Windows Installer program for an unattended install.

## Windows Installer files
Your installation media contains Windows Installer files for each [!INCLUDE[sma_1](../../includes/sma_1_md.md)] of the following features:

-   PowerShell module: PowershellModuleInstaller.msi

-   Web service: WebServiceInstaller.msi

-   Runbook worker: WorkerInstaller.msi

> [!NOTE]
> The installation options must be entered at a command prompt. An answer file is not supported.

## PowerShell module installation options
The [!INCLUDE[sma_1](../../includes/sma_1_md.md)] PowerShell module is a required prerequisite of the [!INCLUDE[sma_1](../../includes/sma_1_md.md)] web service, so you must install the [!INCLUDE[sma_1](../../includes/sma_1_md.md)] PowerShell module before you deploy the [!INCLUDE[sma_1](../../includes/sma_1_md.md)] web service. The PowerShell module installer takes no parameters. For example, you could use the following command:

```
msiexec.exe /i PowershellModuleInstaller.msi
```

## Web service installation options
The following variables can be specified at a command prompt to override default behaviors.

||||
|-|-|-|
|**Installation item**|**Command line switch**|**Valid values**|
|IIS application pool|APPOOLACCOUNT|String|
|IIS application pool|APPOOLPASSWORD|String|
|IIS application pool|ADMINGROUPMEMBERS|String \(a comma\-separated list of users to add to the IIS Administrators group\)|
|SQL Server database|CREATEDATABASE|"Yes" or "No" \(the default value is "No"\)|
|SQL Server database|DATABASEAUTHENTICATION|SQL, Windows \(the default value is Windows\). If DATABASEAUTHENTICATION \= SQL, you must also specify SQLUSER and SQLPASSWORD|
|SQL Server database|SQLUSER|String|
|SQL Server database|SQLPASSWORD|String|
|SQL Server database|SQLSERVER|In the format "Server name, port number." \(The default values are “localhost, 1433.” Supply a port number of 0 to specify a dynamic port.\)|
|SQL Server database|SQLINSTANCE|String \(optional server instance name\)|
|SQL Server database|SQLDATABASE|String \(the default database name value is SMA\)|
|IIS web service|SITENAME|String \(the default value is "SMA"\)|
|IIS web service|WEBSERVICEPORT|Integer \(the default value is "9090"\)|
|IIS web service|INSTALLFOLDER|String \(the default value is c:\\inetpub\\Service Management Automation\)|
|IIS web service|USESSL|“Yes” or “No” \(the default value is “Yes”\)|
|IIS web service|SPECIFYCERTIFICATE|“Yes” or “No” \(the default value is “No”\). A certificate is automatically created if you specify "No." If you select "Yes," also provide CERTIFICATESERIAL.|
|IIS web service|CERTIFICATESERIAL|Serial number of an existing certificate in concatenated hexadecimal format and with no spaces between digits, for example: “45C324C02318F48D4A9C4FC832B2CDCC”|
|Event tracing \(ETW\)|ETWMANIFEST|“Yes” or “No” \(the default value is “Yes”\)|
|Software Quality Metrics \(SQM\) for Customer Experience Improvement Program \(CEIP\) reporting|SENDCEIPREPORTS|“Yes” or “No” \(the default value is “No”\)|
|Automatic Microsoft Update|MSUPDATE|“Yes” \(opt\-in\) or “No” \(no change; this is the default value\)|
|Product key|PRODUCTKEY|String|

If logging is desired, use the Msiexec.exe command and specify the log path. For example, you could use the following command \(be sure to use the name of your SQL Server instance\).

```
msiexec.exe /i WebServiceInstaller.msi /L*v C:\Andreas\WebServiceInstaller.log CREATEDATABASE=“Yes” SQLSERVER="localhost" DATABASEAUTHENTICATION="Windows" SQLDATABASE="SMA123"
```

## Runbook worker installation options
A runbook worker cannot be installed on the same computer as another runbook worker. Also, you must install the runbook worker on a computer that has access to the same SQL Server instance that the [!INCLUDE[sma_1](../../includes/sma_1_md.md)] web service is using.

The following variables can be specified at a command prompt to override default behaviors.

||||
|-|-|-|
|**Installation item**|**Command line switch**|**Valid values**|
|Windows service|SERVICEACCOUNT|String|
|Windows service|SERVICEPASSWORD|String|
|SQL Server database|CREATEDATABASE|“Yes” or “No” \(the default value is “No”\)|
|SQL Server database|DATABASEAUTHENTICATION|SQL Server or Windows \(the default value is Windows\)|
|SQL Server database|SQLUSER|String|
|SQL Server database|SQLPASSWORD|String|
|SQL Server database|SQLSERVER|In the format “Server name, port number” \(The default values are “localhost, 1433.” Supply a port number of 0 to specify a dynamic port.\)|
|SQL Server database|SQLINSTANCE|String \(optional server instance name\)|
|SQL Server database|SQLDATABASE|String \(the default database name value is SMA\)|
|File install location|INSTALLFOLDER|String \(the default value is C:\\Program Files\\Microsoft System Center 2012 R2\\Service Management Automation\)|
|Event tracing \(ETW\)|ETWMANIFEST|“Yes” or “No” \(the default value is “Yes”\)|
|Software Quality Metrics \(SQM\) for Customer Experience Improvement Program \(CEIP\) reporting|SENDCEIPREPORTS|“Yes” or “No” \(the default value is “No”\)|
|Automatic Microsoft Update|MSUPDATE|“Yes” \(opt\-in\) or “No” \(no change; this is the default value\)|
|Product key|PRODUCTKEY|String|

If logging is desired, use the Msiexec.exe command and specify the log path. For example, you could use the following command \(be sure to use the name of your SQL Server instance\).

```
msiexec.exe /i WorkerInstaller.msi /L*v C:\Andreas\WorkerInstaller.log CREATEDATABASE=“Yes” SQLSERVER="localhost" DATABASEAUTHENTICATION="Windows" SQLDATABASE="SMA123"
```

> [!NOTE]
> If you install additional runbook workers, you must run the Windows PowerShell cmdlet **New\-SmaRunbookWorkerDeployment** to properly configure the runbook worker.
> 
> 1.  Stop the Runbook server service \(RunbookService.exe\) on each computer on which a runbook worker is installed.
> 2.  Run the following Windows PowerShell command:
> 
>     **New\-SmaRunbookWorkerDeployment \-\<ComputerName\> –\<WebServiceEndpoint\>**
> 3.  Restart the Runbook server service on each computer on which a runbook worker is installed.

## See also
[Deploy Service Management Automation](Deploy-Service-Management-Automation.md)


