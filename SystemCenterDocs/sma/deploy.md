---
description: Provides step by step instructions for setting up Service Management Automation
manager:  carmonm
ms.topic:  article
author:  cfreemanwa
ms.author: cfreeman
ms.prod:  system-center-threshold
keywords:  
ms.date: 03/28/2017
title:  Deploy Service Management Automation
ms.technology:  service-management-automation
ms.assetid:  b6044e0c-0caa-459c-9489-c379a154136b
---

# How to deploy Service Management Automation 

>Applies To: System Center 2016 - Service Management Automation

In order to deploy Service Management Automation (SMA) you must install the SMA Web Service, setup the SMA runbook worker, and setup the SMA PowerShell module. You can also install the Service Management Automation components by using an unattended installation. 

You can install the web service on any machine that can communicate with Windows Azure Pack and an instance of SQL Server.

## To install the Service Automation web service

1.  In the folder where you downloaded the System Center 2016 Orchestrator installation software, click Setup to start the Setup wizard.

2.  Under **Service Management**, click **Web Service**, and then click **Install**.

3.  Complete the product registration information, and then click **Next**.

4.  Review and accept the license terms, and then click **Next**.

5.  Review the Diagnostic and Usage Data Notice, and then click **Next**.

6.  This will launch the prerequisite check. Review the results of the check. If all items are installed, click **Next**.

    > [!NOTE]
    > If you see an X next to any of the prerequisite software, you must install the item, and then run the prerequisite check again. You cannot complete installation of the service endpoint until you pass the prerequisite check.

7.  Provide the following information for the database the endpoint to use, and then click **Next**.

    |**Item** |**Action** |
    |-------------|----------------------|
    | **Server** |Enter the name of the database server. By default, this is localhost.<br /><br />The format is sqlserver\instance, where \instance is optional.|
    | **Port number** |Enter the port number that you want to use for the database. The default is 1433.|
    | **Database name** |Enter the name of the database. The default is SMA.|
    | **Authentication Credentials** |Select the type of authentication that you want to use. You can use Windows authentication or SQL Server authentication.<br /><br />If you choose SQL Server authentication, enter the user name and password for the computer running SQL Server.|

    > [!NOTE]
    > If you are [upgrading from a previous installation](upgrade.md), please use the database details from the previous installation.

8.  Provide the following information to configure the Internet Information Settings (IIS) for the web service, and then click **Next**.

    |**Item** |**Action** |
    |-----------|------------|
    |**Domain security group or users with access** |Enter a security group or one or more users who can grant access to the web service.|
    |**Application pool name** |SMA<br /><br />This name is not configurable.|
    |**Application pool credentials** |Specify the credentials to use for the application pool. These are the credentials that the web service will run under.|

9. Enter the port number for the web service to use. By default, this is 9090.

10. Choose the security certificate to use to encrypt communication between Windows Azure Pack and the Service Management Automation web service endpoint.

    You can have the installer generate a self-signed certificate to use, or you can select an existing certificate in your local certificate store.

    Click **Next**.

11. Review the location for the web service files. You can accept the default or specify a different location. Click **Next**.

12. Indicate whether you want to use Microsoft Update to keep your software up-to-date. Click **Next**.

13. Review the installation summary, and then click **Install**.

    After the installation is complete, install a runbook worker as described in [How to install the Service Management Automation runbook worker](~/sma/deploy.md).

## To install the SMA PowerShell module

1.  In the folder where you downloaded the System Center 2016 Orchestrator installation software, start the Setup wizard.

2.  Under **Service Management**, click **PowerShell administration**, and then click **Install**.

3.  Follow the instructions in the Setup wizard.

## To setup the SMA runbook worker

1.  In the folder where you downloaded the System Center 2016 Orchestrator installation software, click Setup to start the Setup wizard.

2.  Under **Service Management**, click **Runbook Worker**, and then click **Install**.

3.  Follow the instructions in the Setup wizard.

After the installation is complete, use administrative credentials to configure Automation in the Windows Azure Pack management portal.

>[!IMPORTANT]
>Each Service Management Automation component is installed on an Internet Information Services (IIS) website that, by default, is configured with a self-signed certificate. Because these self-signed certificates are not issued by any of the trusted root certification authorities that your browser loads on startup, your browser displays a security warning when you attempt to connect to any of the sites. We recommend that you replace the self-signed certificates with certificates that are issued by a trusted root certification authority to avoid this experience.

## Setup SMA from a command prompt

Your installation media contains Windows Installer files for each Service Management Automation of the following features:

-   PowerShell module: PowershellModuleInstaller.msi

-   Web service: WebServiceInstaller.msi

-   Runbook worker: WorkerInstaller.msi

> [!NOTE]
> The installation options must be entered at a command prompt. An answer file is not supported.

### PowerShell module installation options
The Service Management Automation PowerShell module is a required prerequisite of the Service Management Automation web service, so you must install the Service Management Automation PowerShell module before you deploy the Service Management Automation web service. The PowerShell module installer takes no parameters. For example, you could use the following command:

```
msiexec.exe /i PowershellModuleInstaller.msi
```

### Web service installation options
The following variables can be specified at a command prompt to override default behaviors.



|**Installation item** |**Command line switch** |**Valid values** |
|------------|--------------|--------------|
|IIS application pool|APPOOLACCOUNT|String|
|IIS application pool|APPOOLPASSWORD|String|
|IIS application pool|ADMINGROUPMEMBERS|String (a comma-separated list of users to add to the IIS Administrators group)|
|SQL Server database|CREATEDATABASE|"Yes" or "No" (the default value is "No")|
|SQL Server database|DATABASEAUTHENTICATION|SQL, Windows (the default value is Windows). If DATABASEAUTHENTICATION = SQL, you must also specify SQLUSER and SQLPASSWORD|
|SQL Server database|SQLUSER|String|
|SQL Server database|SQLPASSWORD|String|
|SQL Server database|SQLSERVER|In the format "Server name, port number." (The default values are "localhost, 1433." Supply a port number of 0 to specify a dynamic port.)|
|SQL Server database|SQLINSTANCE|String (optional server instance name)|
|SQL Server database|SQLDATABASE|String (the default database name value is SMA)|
|IIS web service|SITENAME|String (the default value is "SMA")|
|IIS web service|WEBSERVICEPORT|Integer (the default value is "9090")|
|IIS web service|INSTALLFOLDER|String (the default value is c:\inetpub\Service Management Automation)|
|IIS web service|USESSL|"Yes" or "No" (the default value is "Yes")|
|IIS web service|SPECIFYCERTIFICATE|"Yes" or "No" (the default value is "No"). A certificate is automatically created if you specify "No." If you select "Yes," also provide CERTIFICATESERIAL.|
|IIS web service|CERTIFICATESERIAL|Serial number of an existing certificate in concatenated hexadecimal format and with no spaces between digits, for example: "45C324C02318F48D4A9C4FC832B2CDCC"|
|Event tracing (ETW)|ETWMANIFEST|"Yes" or "No" (the default value is "Yes")|
|**Usage and Diagnostics Data sent to Microsoft**|SENDTELEMETRYREPORTS|"Yes" or "No" (the default value is "Yes")|
|Automatic Microsoft Update|MSUPDATE|"Yes" (opt-in) or "No" (no change; this is the default value)|
|Product key|PRODUCTKEY|String|

If logging is desired, use the Msiexec.exe command and specify the log path. For example, you could use the following command (be sure to use the name of your SQL Server instance).

```
msiexec.exe /i WebServiceInstaller.msi /L*v C:\Andreas\WebServiceInstaller.log CREATEDATABASE="Yes" SQLSERVER="localhost" DATABASEAUTHENTICATION="Windows" SQLDATABASE="SMA123"
```

### Runbook worker installation options
A runbook worker cannot be installed on the same computer as another runbook worker. Also, you must install the runbook worker on a computer that has access to the same SQL Server instance that the Service Management Automation web service is using.

The following variables can be specified at a command prompt to override default behaviors.

|**Installation item** |**Command line switch** |**Valid values** |
|---------------|---------------|-------------|
|Windows service|SERVICEACCOUNT|String|
|Windows service|SERVICEPASSWORD|String|
|SQL Server database|CREATEDATABASE|"Yes" or "No" (the default value is "No")|
|SQL Server database|DATABASEAUTHENTICATION|SQL Server or Windows (the default value is Windows)|
|SQL Server database|SQLUSER|String|
|SQL Server database|SQLPASSWORD|String|
|SQL Server database|SQLSERVER|In the format "Server name, port number" (The default values are "localhost, 1433." Supply a port number of 0 to specify a dynamic port.)|
|SQL Server database|SQLINSTANCE|String (optional server instance name)|
|SQL Server database|SQLDATABASE|String (the default database name value is SMA)|
|File install location|INSTALLFOLDER|String (the default value is C:\Program Files\Microsoft System Center 2012 R2\Service Management Automation)|
|Event tracing (ETW)|ETWMANIFEST|"Yes" or "No" (the default value is "Yes")|
|**Usage and Diagnostics Data sent to Microsoft**|SENDTELEMETRYREPORTS|"Yes" or "No" (the default value is "Yes")|
|Automatic Microsoft Update|MSUPDATE|"Yes" (opt-in) or "No" (no change; this is the default value)|
|Product key|PRODUCTKEY|String|

If logging is desired, use the Msiexec.exe command and specify the log path. For example, you could use the following command (be sure to use the name of your SQL Server instance).

```
msiexec.exe /i WorkerInstaller.msi /L*v C:\Andreas\WorkerInstaller.log CREATEDATABASE="Yes" SQLSERVER="localhost" DATABASEAUTHENTICATION="Windows" SQLDATABASE="SMA123"
```

> [!NOTE]
> If you install additional runbook workers, you must run the Windows PowerShell cmdlet **New-SmaRunbookWorkerDeployment** to properly configure the runbook worker.
>
> 1.  Stop the Runbook server service (RunbookService.exe) on each computer on which a runbook worker is installed.
> 2.  Run the following Windows PowerShell command:
>
>     **New-SmaRunbookWorkerDeployment -<ComputerName\> "<WebServiceEndpoint\>**
> 3.  Restart the Runbook server service on each computer on which a runbook worker is installed.
## To set or change the SMA endpoint

The **QuickStart** tab for Automation in Windows Azure Pack for Windows Server provides a link that enables you to set up or change the Service Management Automation endpoint. If the Service Management Automation endpoint is not yet registered, click **Register the Service Management Automation endpoint** to configure it. To change the Service Management Automation endpoint settings after an endpoint has been set up, click **Current Service Management Automation endpoint**.

The Service Management Automation endpoint requires the following information:

-   The service URL and port. The port number is set when you install Service Management Automation.

-   The user name of a user account that can access the Service Management Automation web service. Accounts with access to the Service Management Automation web service are also set during installation.

-   The access password for the user account.

## Uninstall SMA 

Any of the SMA components can be removed in the **Control Panel** by selecting the component in the Programs section and clicking **Uninstall**.

## Next steps

- Learn more about Windows Azure Pack for Windows Server [Windows Azure Pack for Windows Server](https://technet.microsoft.com/en-us/library/dn296435.aspx).
