---
ms.assetid: e305673d-88ab-4aa1-9287-31b617a9f1fc
title: Installing Operations Manager From the Command Prompt
description: This article describes the different command-line arguments you would use when installing an Operations Manager component from the Command Prompt.
author: jyothisuri
manager: evansma
ms.author: jsuri
ms.date: 01/24/2018
ms.custom: na, intro-installation
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Installing Operations Manager from the Command Prompt

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

You can install features of Operations Manager by using the **setup.exe** command in the Command Prompt window. Gateway and agent installations require the use of MOMGateway.msi and MOMAgent.msi. You must ensure that all servers meet the minimum supported configuration requirements for System Center Operations Manager. For more information, see [System Requirements](./system-requirements.md).

## Command-line parameters

The following table lists the command-line parameters for installing features of Operations Manager.

> [!NOTE]
> If the parameter contains a colon, a value is required. Otherwise, it is simply a switch.

|Parameter|Value|
|-------------|---------|
|/ActionAccountUser:|The domain and user name of the Management server action account.<br><br>Used if you do not want to specify the Local System|
|/ActionAccountPassword:|The password for the Management server action account.<br><br>Used if you do not want to specify the Local System.|
|/AcceptEndUserLicenseAgreement:|0: Do not accept the End User License Agreement (EULA).<br><br>1: Accept the End User License Agreement (EULA).<br><br>When performing a clean installation of System Center Operations Manager, this switch is needed for all management servers. It is also needed for other scripted installations.|
|/components|OMServer: install a management server.<br><br>OMConsole: install an Operations console.<br><br>OMWebConsole: install a web console.<br><br>OMReporting: install a Reporting server.|
|/DatabaseName:|The name of the Operational database.|
|/DWSqlServerInstance:|The data warehouse server and instance `<server\instance>` or Always On availability group listener.|
|/DWSqlInstancePort:| The SQL server instance port number.|
|/DWDatabaseName:|The name of the data warehouse database.|
|/DASAccountUser:|The domain and user name of the Data Access service account.<br><br>Used if you do not want to specify the Local System.|
|/DASAccountPassword:|The password for the Data Access service account.<br><br>Used if you do not want to specify the Local System.|
|/DataReaderUser:|The domain and user name of the data reader account.|
|/DataReaderPassword:|The password for the data reader account.|
|/DataWriterUser:|The domain and user name of the data writer account.|
|/DataWriterPassword:|The password for the data writer account.|
|/EnableErrorReporting:|Never: Do not opt in to sending automatic error reports.<br><br>Queued: Opt in to sending error reports, but queue the reports for review before sending.<br><br>Always: Opt in to automatically send error reports.|
|/install|Runs an installation. Use **/components** to indicate specific features to install.|
|/InstallPath:|Runs an installation specifying an alternative location, to Change the default path for install to another drive.  For example: `/InstallPath: "D:\Program Files\System Center\Operations Manager"` to change from the default location of drive C.|
|/ManagementServer:|Used to specify the name of the management server associated with a web console and/or Reporting server that is not installed on a management server.|
|/ManagementGroupName:|The name of the management group|
|/ManagementServicePort:|Change the Management Server port on install|
|/recover|Recover the Operations Manager Management Server. This will check if any other Management Servers in the Management Group are still online. If another Management Server is found online, the Setup will attempt to contact them and copy the registry entries needed to deal with RunAs Account Decryption. <br><br> If there are not any Management Servers detected, the Setup will re-generate a new decryption key. You will need to re-enter your existing RunAs Account passwords after the recovery completes.|
|/silent|Does not display the installation wizard.|
|/SqlServerInstance:|The SQL server and instance `<server\instance>` or Always On availability group listener.|
|/SqlInstancePort:| The SQL server instance port number.|
|/SendCEIPReports:|0: Do not opt in to the Customer Experience Improvement Program (CEIP).<br><br>1: Opt in to CEIP.|
|/SRSInstance:|The reporting server and instance (<server\instance>).<br><br>Used for Reporting Server installations.|
|/SendODRReports:|0: Do not opt in to sending operational data reports.<br><br>1: opt in to sending operational data reports.<br><br>Used for Reporting Server Installations.|
|/UseLocalSystemActionAccount|Used to specify the Local System for the Management server action account.|
|/UseLocalSystemDASAccount|Used to specify the Local System for the Data Access service account.|
|/UseMicrosoftUpdate:|0: Do not opt in to Microsoft Update.<br><br>1: Opt in to Microsoft Update.|
|/uninstall|Uninstalls Operations Manager. Use **/components** to indicate specific features to uninstall. If **/components** is not specified, it will uninstall all features of Operations Manager on the server.|
|/WebSiteName:|The name of the website. For default web installation, specify "**Default Web Site**".<br><br>Used for web console installations.|
|/WebConsoleUseSSL|Specify only if your website has Secure Sockets Layer (SSL) activated.<br><br>Used for web console installations.|
|/WebConsoleAuthorizationMode:|Mixed: Used for intranet scenarios.<br><br>Network: Used for extranet scenarios.<br><br>Used for web console installations.|


## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing each one of the features across multiple servers in your management group.
