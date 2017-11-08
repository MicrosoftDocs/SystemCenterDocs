---
ms.assetid: e305673d-88ab-4aa1-9287-31b617a9f1fc
title: Installing Operations Manager From the Command Prompt 
description: This article describes the different command-line arguments you would use when installing an Operations Manager component from the Command Prompt. 
author: mgoedtel
manager: carmonm
ms.date: 01/26/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Installing Operations Manager from the Command Prompt 

You can install features of Operations Manager by using the **setup.exe** command in the Command Prompt window. Gateway and agent installations require the use of MOMGateway.msi and MOMAgent.msi. You must ensure that all servers meet the minimum supported configuration requirements for System Center 2016 - Operations Manager. For more information, see [System Requirements](../orchestrator/system-requirements.md).

## Command-line parameters

The following table lists the command-line parameters for installing features of Operations Manager.

> [!NOTE]
> If the parameter contains a colon, a value is required. Otherwise, it is simply a switch.

|Parameter|Value|
|-------------|---------|
|/silent|Does not display the installation wizard.|
|/install|Runs an installation. Use **/components** to indicate specific features to install.|
|/InstallPath|Runs an installation specifying an alternative location, to Change the default path for install to another drive.  For example: `/InstallPath: "D:\Program Files\System Center Operations Manager 2016"` to change from the default location of drive C.|
|/components|OMServer: install a management server.<br><br>OMConsole: install an Operations console.<br><br>OMWebConsole: install a web console.<br><br>OMReporting: install a Reporting server.|
|/ManagementGroupName:|The name of the management group|
|/ManagementServicePort:|Change the Management Server port on install|
|/SqlServerInstance:|The SQL server and instance `<server\instance>` or Always On availability group listener.|
|/SqlInstancePort:| The SQL server instance port number.|
|/DatabaseName:|The name of the Operational database.|
|/DWSqlServerInstance:|The data warehouse server and instance `<server\instance>` or Always On availability group listener.|
|/DWSqlInstancePort:| The SQL server instance port number.|
|/DWDatabaseName:|The name of the data warehouse database.|
|/UseLocalSystemActionAccount|Used to specify the Local System for the Management server action account.|
|/ActionAccountUser:|The domain and user name of the Management server action account.<br><br>Used if you do not want to specify the Local System|
|/ActionAccountPassword:|The password for the Management server action account.<br><br>Used if you do not want to specify the Local System.|
|/UseLocalSystemDASAccount|Used to specify the Local System for the Data Access service account.|
|/DASAccountUser:|The domain and user name of the Data Access service account.<br><br>Used if you do not want to specify the Local System.|
|/DASAccountPassword:|The password for the Data Access service account.<br><br>Used if you do not want to specify the Local System.|
|/DataReaderUser:|The domain and user name of the data reader account.|
|/DataReaderPassword:|The password for the data reader account.|
|/DataWriterUser:|The domain and user name of the data writer account.|
|/DataWriterPassword:|The password for the data writer account.|
|/EnableErrorReporting:|Never: Do not opt in to sending automatic error reports.<br><br>Queued: Opt in to sending error reports, but queue the reports for review before sending.<br><br>Always: Opt in to automatically send error reports.|
|/SendCEIPReports:|0 : Do not opt in to the Customer Experience Improvement Program (CEIP).<br><br>1 : Opt in to CEIP.|
|/UseMicrosoftUpdate:|0 : Do not opt in to Microsoft Update.<br><br>1 : Opt in to Microsoft Update.|
|/AcceptEndUserLicenseAgreement:|0 : Do not accept the End User License Agreement (EULA).<br><br>1 : Accept the End User License Agreement (EULA).<br><br>When performing a clean installation of System Center 2016 - Operations Manager, this switch is needed for all management servers. It is also needed for other scripted installations.|
|/ManagementServer|Used to specify the name of the management server associated with a web console and/or Reporting server that is not installed on a management server.|
|/WebSiteName:|The name of the website. For default web installation, specify "**Default Web Site**".<br <br>Used for web console installations.|
|/WebConsoleUseSSL|Specify only if your website has Secure Sockets Layer (SSL) activated.<br><br>Used for web console installations.|
|/WebConsoleAuthorizationMode:|Mixed: Used for intranet scenarios.<br><br>Network: Used for extranet scenarios.<br><br>Used for web console installations.|
|/SRSInstance|The reporting server and instance (<server\instance>).<br><br>Used for Reporting Server installations.|
|/SendODRReports:|0: Do not opt in to sending operational data reports.<br><br>1: opt in to sending operational data reports.<br><br>Used for Reporting Server Installations.|
|/uninstall|Uninstalls Operations Manager. Use **/components** to indicate specific features to uninstall. If **/components** is not specified, it will uninstall all features of Operations Manager on the server.|

## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing each one of the features across multiple servers in your management group.  

