---
description: Provides step by step instructions for setting up Service Management Automation.
ms.topic: install-set-up-deploy
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
ms.date: 08/20/2025
title: Deploy Service Management Automation
ms.subservice: service-management-automation
ms.custom: UpdateFrequency2, intro-deployment, engagement-fy24
ms.update-cycle: 1095-days
---

# Deploy Service Management Automation

To deploy Service Management Automation (SMA), you must install the SMA Web Service, set up the SMA runbook worker, and set up the SMA PowerShell module. You can also install the Service Management Automation components by using an unattended installation.

You can install the web service on any machine that can communicate with Windows Azure Pack and an instance of SQL Server.

>[!NOTE]
>As Windows Azure Pack is now deprecated, you can use PowerShell ISE add-on as an alternative. For more information, see [Introducing Service Management Automation ISE add-on](https://techcommunity.microsoft.com/blog/systemcenterblog/introducing-service-management-automation-ise-add-on/351500).

## Install the Service Automation web service

1. In the folder containing the downloaded System Center - Orchestrator installation software, select **Setup** to start the Setup wizard.

2. Under **Service Management**, select **Web Service**, and select **Install**.

3. Complete the product registration information, and select **Next**.

4. Review and accept the license terms, and select **Next**.

5. Review the Diagnostic and Usage Data Notice, and select **Next**.

6. This launches the prerequisites check. Review the results of the check. If all the items are installed, select **Next**.

    > [!NOTE]
    > If you see an X next to any of the prerequisite software, you must install the item, and then run the prerequisite check again. You can't complete the installation of the service endpoint until you pass the prerequisite check.

7. Provide the following information for the database endpoint to use, and select **Next**.

    |**Item** |**Action** |
    |-------------|----------------------|
    | **Server** |Enter the name of the database server. By default, this is localhost.<br/><br/>The format is sqlserver\instance, where \instance is optional.|
    | **Port number** |Enter the port number that you want to use for the database. The default is 1433.|
    | **Database name** |Enter the name of the database. The default is SMA.|
    | **Authentication Credentials** |Select the type of authentication that you want to use. You can use Windows authentication or SQL Server authentication.<br/><br/>If you choose SQL Server authentication, enter the user name and password for the computer running SQL Server.|

    > [!NOTE]
    > If you're [upgrading from a previous installation](./upgrade-sma.md), use the database details from the previous installation.

8. Provide the following information to configure the Internet Information Settings (IIS) for the web service, and select **Next**.

    |**Item** |**Action** |
    |-----------|------------|
    |**Domain security group or users with access** |Enter a security group or one or more users who can grant access to the web service.|
    |**Application pool name** |SMA<br/><br/>This name isn't configurable.|
    |**Application pool credentials** |Specify the credentials to use for the application pool. These are the credentials that the web service will run under.|

9. Enter the port number for the web service to use. By default, this is 9090.

10. Choose the security certificate to use to encrypt communication between Windows Azure Pack and the SMA web service endpoint.

    You can have the installer generate a self-signed certificate to use, or you can select an existing certificate in your local certificate store.

    Select **Next**.

11. Review the location for the web service files. You can accept the default or specify a different location. Select **Next**.

12. Indicate whether you want to use Microsoft Update to keep your software up-to-date. Select **Next**.

13. Review the installation summary, and select **Install**.

    After the installation is complete, install a runbook worker as described in [How to install the SMA runbook worker](~/sma/deploy.md).

## Install the SMA PowerShell module

1. In the folder containing the downloaded System Center Orchestrator installation software, start the Setup wizard.

2. Under **Service Management**, select **PowerShell administration**, and select **Install**.

3. Follow the instructions in the Setup wizard.

## Set up the SMA runbook worker

1. In the folder containing the downloaded Orchestrator installation software, select Setup to start the Setup wizard.

2. Under **Service Management**, select **Runbook Worker**, and select **Install**.

3. Follow the instructions in the Setup wizard.

After the installation is complete, use the administrative credentials to configure Automation in the Windows Azure Pack management portal.

>[!IMPORTANT]
>Each SMA component is installed on an Internet Information Services (IIS) website that, by default, is configured with a self-signed certificate. Because these self-signed certificates are not issued by any of the trusted root certification authorities that your browser loads on startup, your browser displays a security warning when you attempt to connect to any of the sites. We recommend that you replace the self-signed certificates with certificates that are issued by a trusted root certification authority to avoid this experience.

## Set up SMA from a command prompt

Your installation media contains Windows Installer files for each SMA of the following features:

- PowerShell module: PowershellModuleInstaller.msi

- Web service: WebServiceInstaller.msi

- Runbook worker: WorkerInstaller.msi

> [!NOTE]
> The installation options must be entered at a command prompt. An answer file isn't supported.

### PowerShell module installation options

The SMA PowerShell module is a required prerequisite of the SMA web service, so you must install the SMA PowerShell module before you deploy the SMA web service. The PowerShell module installer takes no parameters. For example, you could use the following command:

```powershell
msiexec.exe /i PowershellModuleInstaller.msi
```

### Web service installation options

The following variables can be specified at a command prompt to override default behaviors.

|**Installation item** |**Command-line switch** |**Valid values** |
|------------|--------------|--------------|
|IIS application pool|APPOOLACCOUNT|String|
|IIS application pool|APPOOLPASSWORD|String|
|IIS application pool|ADMINGROUPMEMBERS|String (a comma-separated list of users to add to the IIS Administrators group)|
|SQL Server database|CREATEDATABASE|**Yes** or **No** (the default value is **No**)|
|SQL Server database|DATABASEAUTHENTICATION|SQL, Windows (the default value is Windows). If DATABASEAUTHENTICATION = SQL, you must also specify SQLUSER and SQLPASSWORD|
|SQL Server database|SQLUSER|String|
|SQL Server database|SQLPASSWORD|String|
|SQL Server database|SQLSERVER|In the format **Server name, port number.** (The default values are **localhost, 1433**. Supply a port number of 0 to specify a dynamic port.)|
|SQL Server database|SQLINSTANCE|String (optional server instance name)|
|SQL Server database|SQLDATABASE|String (the default database name value is SMA)|
|IIS web service|SITENAME|String (the default value is **SMA**)|
|IIS web service|WEBSERVICEPORT|Integer (the default value is **9090**)|
|IIS web service|INSTALLFOLDER|String (the default value is c:\inetpub\Service Management Automation)|
|IIS web service|USESSL|**Yes** or **No** (the default value is **Yes**)|
|IIS web service|SPECIFYCERTIFICATE|**Yes** or **No** (the default value is **No**). A certificate is automatically created if you specify **No**. If you select **Yes**, also provide CERTIFICATESERIAL.|
|IIS web service|CERTIFICATESERIAL|Serial number of an existing certificate in concatenated hexadecimal format and with no spaces between digits; for example: **45C324C02318F48D4A9C4FC832B2CDCC**|
|Event tracing (ETW)|ETWMANIFEST|**Yes** or **No** (the default value is **Yes**)|
|**Usage and Diagnostics Data sent to Microsoft**|SENDTELEMETRYREPORTS|**Yes** or **No** (the default value is **Yes**)|
|Automatic Microsoft Update|MSUPDATE|**Yes** (opt-in) or **No** (no change; this is the default value)|
|Product key|PRODUCTKEY|String|

If logging is desired, use the Msiexec.exe command and specify the log path. For example, you could use the following command (ensure to use the name of your SQL Server instance).

```powershell
msiexec.exe /i WebServiceInstaller.msi /L*v C:\Andreas\WebServiceInstaller.log CREATEDATABASE="Yes" SQLSERVER="localhost" DATABASEAUTHENTICATION="Windows" SQLDATABASE="SMA123"
```

### Runbook worker installation options

A runbook worker can't be installed on the same computer as another runbook worker. Also, you must install the runbook worker on a computer that has access to the same SQL Server instance that the SMA web service is using.

The following variables can be specified at a command prompt to override default behaviors.

|**Installation item** |**Command-line switch** |**Valid values** |
|---------------|---------------|-------------|
|Windows service|SERVICEACCOUNT|String|
|Windows service|SERVICEPASSWORD|String|
|SQL Server database|CREATEDATABASE|**Yes** or **No** (the default value is **No**)|
|SQL Server database|DATABASEAUTHENTICATION|SQL Server or Windows (the default value is Windows)|
|SQL Server database|SQLUSER|String|
|SQL Server database|SQLPASSWORD|String|
|SQL Server database|SQLSERVER|In the format **Server name, port number** (The default values are **localhost, 1433**. Supply a port number of 0 to specify a dynamic port.)|
|SQL Server database|SQLINSTANCE|String (optional server instance name)|
|SQL Server database|SQLDATABASE|String (the default database name value is SMA)|
|File installation location|INSTALLFOLDER|String (the default value is C:\Program Files\Microsoft System Center \<version\>\Service Management Automation)|
|Event tracing (ETW)|ETWMANIFEST|**Yes** or **No** (the default value is **Yes**)|
|**Usage and Diagnostics Data sent to Microsoft**|SENDTELEMETRYREPORTS|**Yes** or **No** (the default value is **Yes**)|
|Automatic Microsoft Update|MSUPDATE|**Yes** (opt-in) or **No** (no change; this is the default value)|
|Product key|PRODUCTKEY|String|

If logging is desired, use the Msiexec.exe command and specify the log path. For example, you could use the following command (ensure to use the name of your SQL Server instance):

```powershell
msiexec.exe /i WorkerInstaller.msi /L*v C:\Andreas\WorkerInstaller.log CREATEDATABASE="Yes" SQLSERVER="localhost" DATABASEAUTHENTICATION="Windows" SQLDATABASE="SMA123"
```

> [!NOTE]
> If you install additional runbook workers, you must run the Windows PowerShell cmdlet **New-SmaRunbookWorkerDeployment** to properly configure the runbook worker.
>
> 1. Stop the Runbook server service (RunbookService.exe) on each computer on which a runbook worker is installed.
> 2. Run the following Windows PowerShell command:
>
>     **New-SmaRunbookWorkerDeployment -<ComputerName\> "<WebServiceEndpoint\>**
> 3. Restart the Runbook server service on each computer on which a runbook worker is installed.

## Set or change the SMA endpoint

The **QuickStart** tab for Automation in Windows Azure Pack for Windows Server provides a link that enables you to set up or change the SMA endpoint. If the Service Management Automation endpoint isn't yet registered, select **Register the Service Management Automation endpoint** to configure it. To change the SMA endpoint settings after an endpoint has been set up, select **Current Service Management Automation endpoint**.

The SMA endpoint requires the following information:

- The service URL and port. The port number is set when you install SMA.

- The username of a user account that can access the SMA web service. Accounts with access to the SMA web service are also set during installation.

- The access password for the user account.

## Uninstall SMA

Any of the SMA components can be removed in the **Control Panel** by selecting the component in the Programs section and selecting **Uninstall**.

## Next steps

Learn more about Windows Azure Pack for Windows Server [Windows Azure Pack for Windows Server](/previous-versions/azure/windows-server-azure-pack/dn296435(v=technet.10)).
