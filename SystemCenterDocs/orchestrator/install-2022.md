---
title: Install System Center Orchestrator 2022
description: Provides instructions for installing System Center - Orchestrator
author: jyothisuri
manager: evansma
ms.date: 03/21/2022
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
ms.author: jsuri
ms.custom: intro-installation
MonikerRange: 'sc-orch-2022'
---

# How to install System Center 2022 - Orchestrator

A complete Orchestrator installation includes a management server, one or more runbook servers, a SQL Server for hosting the Orchestrator database, a web server for hosting the Orchestrator web service, and a server for hosting the Runbook Designer and Runbook Tester. It is possible to install all these roles on a single computer, but it is more common to distribute the roles across several computers or virtual machines.

For a detailed description of the Orchestrator architecture, see [Learn about Orchestrator](learn-about-orchestrator.md).

This topic provides detailed installation instructions for the various Orchestrator roles.

## Install an Orchestrator management server

1.  On the server where you want to install Orchestrator, start the Orchestra Setup Wizard.

    To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!IMPORTANT]
    > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center - Service Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

    > [!NOTE]
    > If User Account Control is enabled, then you will be prompted to verify that you want to allow the setup program to run. This is because it requires administrative access to make changes to the system.

2.  On the main page of the wizard, click **Install**.

3.  On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

    > [!NOTE]
    > For this evaluation release, a product key is not required.

4.  On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5.  On the **Select features to install** page, ensure that **Management Server** is the only feature selected, and then click **Next**.

6.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

   If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:


1. Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

   > [!WARNING]
   > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

2. After you resolve the missing prerequisites, click **Verify prerequisites again**.

3. Click **Next** to continue.

4. On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Click **Test** to verify the account credentials. If the credentials are accepted, then click **Next**.

5. On the **Configure the database server** page, enter the name of the server and the name of the instance of Microsoft SQL Server that you want to use for Orchestrator. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

6. On the **Configure the database** page, select a database or create a new database, and then click **Next**.

7. On the **Configure Orchestrator users group** page, accept the default configuration or enter the name of the Active Directory user group to manage Orchestrator, and then click **Next**.

8. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and then click **Next**.

9. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

10. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

11. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

12. On the **Setup completed successfully** page, optionally indicate whether you want to start Runbook Designer, and then click **Close** to complete the installation.

## Install an Orchestrator runbook server

1. On the server where you want to install an Orchestrator runbook server, start the Orchestrator Setup Wizard.

   To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

   > [!NOTE]
   > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center - Service Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2. On the main setup page, under **Standalone installations**, click **Runbook server**.

3. On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

   > [!NOTE]
   > For this evaluation release, a product key is not required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5. Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

   If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

      > [!WARNING]
      > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer may require a restart. If you restart your computer, you must run setup again from the beginning.

   2. After you resolve the missing prerequisites, click **Verify prerequisites again**.

   3. Click **Next** to continue.

6. On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Click **Test** to verify the account credentials. If the credentials are accepted, click **Next**.

7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

8. On the **Configure the database** page, select the Orchestrator database for your deployment, and then click **Next**.

9. On the **Select the installation location** page, verify the installation location for Orchestrator, and then click **Next**.

10. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

11. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

12. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

13. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.

## Install the Orchestrator Web API service

Since Orchestrator 2022, the Web API service and Orchestration Console can be installed separately, on different machines.

1. On the server where you want to install the Orchestrator web service, start the Orchestrator Setup Wizard.

   To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

   > [!NOTE]
   > Before you begin the installation of the Orchestrator Web API service, close any open programs and ensure that there are no pending restarts on the computer. Then log on to the computer with the same user account to finish the installation of the server role or the security update.


2. On the main setup page, under **Standalone installations**, click **Web API Service**.

3. On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

   > [!NOTE]
   > For this evaluation release, a product key is not required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5. Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

   If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that did not pass the prerequisite check. The Web API requires .NET Hosting bundle v5.x and some IIS extensions. Download and install them from the official sites:
      1.	.NET Hosting bundle
      2.	IIS CORS module

   2. After you resolve the missing prerequisites, click **Verify prerequisites again**.

   3. Click **Next** to continue.

6. On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. The Web API will run under an IIS App Pool with this identity. Click **Test** to verify the account credentials. If the credentials are accepted, click **Next**.

7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. . If Windows Authentication is selected, the service account credentials from previous step are used to connect to the database. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

8. On the **Configure the database** page, select the Orchestrator database for your deployment, and then click **Next**.

9. On the **Configure CORS and the port for the Web API** page, verify the port numbers for the Orchestrator Web API service and the URL of the Orchestration console, and then click **Next**.

10. On the **Select the installation location** page, verify the installation location for Orchestrator, and then click **Next**.

11. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

12. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

13. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

## Install Orchestration Console on a single computer

Since Orchestrator 2022, the Web API service and Orchestration Console can be installed separately, on different machines.

1.	On the server where you want to install the Orchestrator web service, start the Orchestrator Setup Wizard.To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

2.	On the main **Setup** page, under **Standalone installations**, click **Orchestration Console**.

3.	On the **Product registration** page, provide the name and company for the product registration, and click **Next**.

    >[!NOTE]
    >For this evaluation release, a product key is not required.

4.	On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and click **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and click **Next**.

5.	Your computer is checked for required hardware and software. If your computer meets all of the requirements, **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    Orchestration Console requires IIS URL Rewrite module, download from here.

6.	On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. The Console will run under an IIS App Pool with this identity. Click **Test to verify the account credentials**. If the credentials are accepted, click **Next**.

7.	On the **Configure the ports for the Web Console** page, verify the port numbers for the Orchestration Console service and the URL of the Web API service, and click **Next**.

    >[!NOTE]
    >The Web API URL should not have a trailing forward slash `/`.

8.	On the **Select the installation location** page, verify the installation location for Orchestrator, and click **Next**.

9. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and click **Next**.

10. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in Error Reporting, and then click **Next**.

11. Review the **Installation summary** page, and click **Install**.

The **Installing features** page appears and displays the installation progress.

## Install the Orchestrator Runbook Designer on a single computer

1.  On the server where you want to install the Orchestrator Runbook Designer, start the Orchestrator Setup Wizard.

    To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin the install of the Runbook Designer, close any open programs and ensure that there are no pending restarts on the computer. Then, log on to the computer with the same user account to finish the installation of the server role or the security update.


2.  On the main wizard page, click **Runbook Designer**.

3. On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

      > [!NOTE]
      > For this evaluation release, a product key is not required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5. Your computer is checked for required hardware and software. If your computer meets all of the requirements, proceed to the next step.

   If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

   2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

   3.  Click **Next** to continue.

6. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and then click

7. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

8. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

9. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

10. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.


## Connect a Runbook Designer to a management server

1.  In the Runbook Designer, select the **Connect to a server** icon in the navigation pane under the **Connections** pane.

    > [!NOTE]
    > If the Runbook Designer is connected to another management server, the **Connect to a server** icon is disabled. Click the **Disconnect** icon before you connect to a different management server.

2.  In **System Center Orchestrator Connection**, enter the name of the server that hosts your Orchestrator management server, and then click **OK**.

## Enable network discovery

1.  On the desktop of your computer running Windows server, click **Start**, click **Control Panel**, click **Network and Internet**, click **Network and Sharing Center**, click **Choose Home group and Sharing Options**, and then click **Change advanced sharing settings**.

2.  To change the **Domain** profile, if needed, click the **Arrow** icon to expand the section options and make any necessary changes.

3.  Select **Turn on network discovery**, and then click **Save changes**.

    If you are prompted for an administrator password or confirmation, type the password or provide confirmation.

## Install from the command prompt


To install Orchestrator at a command prompt, use Setup.exe with the command-line options in the following table.

|Option|Description|
|----------|---------------|
|/Silent|Installation is performed without displaying a dialog box.|
|/Uninstall|Product is uninstalled. This option is performed silently.|
|/Key:[Product Key]|Specifies the product key. If no product key is specified, Orchestrator is installed as an evaluation edition.|
|/ServiceUserName:[User Name]|Specifies the user account for the Orchestrator Management Service. This value is required if you are installing Management Server, Runbook Server, or web services.|
|/ServicePassword:[Password]|Specifies the password for the user account for the Orchestrator Management Service. This value is required if you are installing Management Server, Runbook Server, or web services.|
|/Components:[Feature 1, Feature 2,"]|Specifies the features to install(comma separated). Possible values are ManagementServer, RunbookServer, RunbookDesigner, WebAPI, WebConsole and All.|
|/InstallDir:[Path]|Specifies the path to install Orchestrator. If no path is specified, C:\Program Files \Microsoft System Center <version>\Orchestrator is used.|
|/DbServer:[Computer[\Instance]]|Specifies the computer name and instance of the database server. This value is required if you are installing Management Server, Runbook Server, or web services.|
|/DbUser:[User Name]|Specifies the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, no value should be specified.|
|/DbPassword:[Password]|Specifies the password for the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, then no value should be specified.|
|/DbNameNew:[Database Name]|Specifies the database name if a new database is being created. Cannot be used with DbNameExisting.|
|/DbNameExisting:[Database Name]|Specifies the database name if an existing database is being used. Cannot be used with DbNameNew.|
|/WebServicePort:[Port]|Specifies the port to use for the Web API service. Required if Web API service is installed.|
|/WebConsolePublicUrl: [URL]|Specifies the URL of the Orchestration Console that should be used to configure CORS on the Web API. Required if Web API service is installed.|
|/WebConsolePort:[Port]|Specifies the port to use for the Orchestrator console. Required if Orchestrator Console is installed.|
|/WebServicePublicUrl:[URL]|Specifies the URL of the web API service that should be used by the Orchestration Console. Required if Orchestration Console is installed.|
|/OrchestratorUsersGroup:[Group SID]|Specifies the SID of the domain or local group that will be granted access to Management server. If no value is specified, the default local group is used.|
|/OrchestratorRemote|Specifies that remote access should be granted to the Runbook Designer.|
|/UseMicrosoftUpdate:[0&#124;1]|Specifies whether to opt in for Microsoft Update. A value of 1 will opt in. A value of 0 does not change the current opt in status of the computer.|
|/SendTelemetryReports:[0&#124;1]|Specifies Orchestrator to send Diagnostics and Usage data to Microsoft. 0 to opt-out from sending Telemetry. **Telemetry is on by default.**|
|/EnableErrorReporting:[value]|Specifies that Orchestrator should send program error reports to Microsoft. Possible values are always, queued, and never.|

For example, you could use the following command to install all of the Orchestrator components using Windows Authentication.

```
.\Setup.exe /Silent /ServiceUserName:<UserName> /ServicePassword:<password> /Components:All /DbServer:<DBServerName> /DbNameNew:Orchestrator /WebServicePort:81 /WebConsolePublicUrl:”http://localhost:82” /WebConsolePort:82 /WebServicePublicUrl:”http://localhost:81”   /UseMicrosoftUpdate:1 /SendTelemetryReports:1 /EnableErrorReporting:always
```
## View runbook server properties

The properties for a runbook server include an optional description and the account information to use for the Runbook Service. You can modify the description but can only view the service credentials.    

1.  In the **Connections**  pane, select the Runbook Servers folder. In the right pane, right-click the runbook server to select **Properties**.  

2.  If you want to add or change the **Description** box, type a description for this runbook server, and then click **Finish**.


## Troubleshoot your installation

The following information provides additional instructions and caveats that you can use during installation to resolve problems you might experience.  

### Orchestrator log files  
If you experience problems during installation, installation log files are located in the folder **C:\\Users\\%USERNAME%\\AppData\\Local\\SCO\\LOGS**.  

If you experience problems when you are running Orchestrator, the product log files are located in the folder **C:\\ProgramData\\Microsoft System Center <version>\\Orchestrator\\**.  

### Windows Firewall  
When you deploy additional Runbook Designer applications to your environment, you might see a failed installation message. To correctly install the Runbook Designer, enable the following firewall rules as they apply to your operating system and deployment configuration.  

### Windows Firewall with advanced security
By default, **Windows Firewall with Advanced Security** is enabled on all Windows Servercomputers, and blocks all incoming traffic unless it is a response to a request by the host, or it is specifically allowed. You can explicitly allow traffic by specifying a port number, application name, service name, or other criteria by configuring Windows Firewall with Advanced Security settings.  

Enable the following rules to allow all Monitor Event activities to function correctly:  

-   Windows Management Instrumentation \(Async\-In\)  

-   Windows Management Instrumentation \(DCOM\-In\)  

-   Windows Management Instrumentation \(WMI\-In\)  

### Automated deployment  
When a runbook server or Runbook Designer is installed behind a firewall, specific firewall rules are required between the remote computers that are used to deploy the runbook server and Runbook Designer. An additional rule is required for the remote connection between the Runbook Designer and the runbook server to allow the Orchestrator management service to accept remote connections. If you are using the **Monitor WMI** task, the runbook server requires a special firewall rule on the computer that uses PolicyModule.exe.  

Enable the following firewall rules on your computer:  

#### Firewall rule between the Runbook Designer and the Orchestrator management server  

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center <version>\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|   

#### Firewall rules between remote computers  

|Operating system|Firewall rules|  
|--------------------|------------------|  
|Windows Server | - File and Printer Sharing<br>- Windows Management Instrumentation \(WMI\)<br>- Program rule for OrchestratorRemotingService to accept remote connections. This rule must be enabled through the Advanced Firewall mode for path %ProgramFiles%\Microsoft System Center \Orchestrator\Management Server\Deployment Manager\OrchestratorRemotingService.exe|

#### Firewall rules between the runbook server and the computer that uses PolicyModule.exe  

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles%\\Microsoft System Center <version>\\Orchestrator\\Runbook Server\\PolicyModule.exe|  
|32\-bit|%ProgramFiles\\Microsoft System Center <version>\\Orchestrator\\Runbook Server\\PolicyModule.exe|  

For more information about adding firewall rules, see [Add or Edit a Firewall Rule](/previous-versions/orphan-topics/ws.11/cc753558(v=ws.11)).  

### <a name="BKMK_RunbookServicefailstostart"></a>RunbookService fails to start after computer reboot  
When you reboot your runbook server, the RunbookService attempts to connect to the orchestration database. If the database is not available, the RunbookService fails. The event log message is **This computer was unable to communicate with the computer providing the server.**. Typically, this can occur when the SQL server and the runbook server are installed on the same computer.  

To solve this problem. you can manually start the RunbookService, or configure the RunbookService to make multiple attempts during startup to connect to database before failing.  

### Cannot restart runbook service if you uninstall with an account without administrator permissions  
If you attempt to uninstall Orchestrator while logged in with an account that is a member of OrchestratorSystemGroup but is not an administrator, uninstall removes all accounts from OrchestratorSystemGroup. If you stop the runbook service and attempt to restart the service, the service fails because the user account does not have the correct permissions to retrieve the orchestration database connection. An account that is an administrator or a member of the OrchestratorSystemGroup is required to retrieve the orchestration database connection.  

To solve this problem, an administrator can add the user back to OrchestratorSystemGroup.

## Next steps

- To learn more about building runbooks see [Design and build runbooks](./design-and-build-runbooks.md).
- To learn more about deploying runbooks see [Deploy runbooks](deploy-runbooks.md)
