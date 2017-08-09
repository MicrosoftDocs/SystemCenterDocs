---
title: Configuration Manager Integration Pack
description: The Integration Pack for Configuration Manager is an add-on for System Center 2016 - Orchestrator that enables you to automate common Configuration Manager functions.
ms.custom: na
ms.date: 03/08/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 4d2feb46-3f4c-4ed6-adbf-50097f94ea61
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Configuration Manager Integration Pack for System Center 2016 - Orchestrator

Applies To: System Center 2016 - Orchestrator

The Integration Pack for Configuration Manager is an add-on for System Center 2016 - Orchestrator that enables you to automate common Configuration Manager management functions.

With this integration pack, you can also create workflows that interact with and transfer information to the integration packs for System Center Service Manager, System Center Data Protection Manager, System Center Operations Manager, and System Center Virtual Machine Manager.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more Orchestrator-related privacy information, see the [Privacy Statement for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

Before you can install the Integration Pack for Configuration Manager, you must first install and configure the following listed software. For more information about how to install and configure Orchestrator and Active Directory, refer to the respective product documentation.

-   System Center 2016 integration packs require System Center 2016 - Orchestrator and System Center 2016 - Configuration Manager.

## Downloading the Integration Pack

To download this integration pack, see [Configuration Manager Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Registering and deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designer. For specific procedures, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Configuring the Configuration Manager Integration Pack connection settings

Connections provide a way for you to define the way that the Configuration Manager Activities will connect to the Configuration Manager server(s) in your infrastructure. You must define at least one connection in order to use the Configuration Manager activities, but you can define as many as you need in order to connect to different Configuration Manager servers or utilize different connection settings or credentials.

### To set up a Configuration Manager connection

1.  In the Runbook Designer, click **Options**, and then click **Configuration Manager**. The **Configuration Manager** dialog box appears.

2.  On the **Connections** tab, click **Add** to begin the connection setup. The **Add Connection** dialog box appears.

3.  In the **Name** box, enter a name for the connection. This could be the name of the *Active Directory* domain, or a descriptive name to distinguish the type of connection.

4.  In the Server box, type the name or IP address of the Configuration Manager computer. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN). If you have installed Orchestrator on the Configuration Manager server, you can type “Localhost” or the NetBIOS name of the server.

5.  In the **Username** and **Password** boxes, type the credentials that Orchestrator will use to connect to the Configuration Manager Site Server. Note that the Username includes the domain name, for example: “contoso\admin”.

6.  Click **Test Connection**. When the message "Successfully connected" appears, click OK.

7. Click OK to close the configuration dialog box, and then click Finish.
