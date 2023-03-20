---
title: Configuration Manager Integration Pack
description: The Integration Pack for Configuration Manager is an add-on for System Center - Orchestrator that enables you to automate common Configuration Manager functions.
ms.custom: UpdateFrequency2
ms.date: 03/08/2017
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d2feb46-3f4c-4ed6-adbf-50097f94ea61
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Configuration Manager Integration Pack for System Center - Orchestrator

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Integration Pack for Configuration Manager is an add-on for System Center - Orchestrator that enables you to automate common Configuration Manager management functions.

With this integration pack, you can also create workflows that interact with and transfer information to the integration packs for System Center Service Manager, System Center Data Protection Manager, System Center Operations Manager, and System Center Virtual Machine Manager.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more Orchestrator-related privacy information, see the [Privacy Statement for System Center - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

Before you can install the Integration Pack for Configuration Manager, you must first install and configure the following listed software. For more information about how to install and configure Orchestrator and Active Directory, see the respective product documentation.

-   System Center integration packs require System Center - Orchestrator and Configuration Manager.

## Downloading the Integration Pack

::: moniker range="<=sc-orch-2019"

- [Download the pack for 2016](https://www.microsoft.com/en-us/download/details.aspx?id=54098)
- [Download the pack for 1801](https://www.microsoft.com/en-us/download/details.aspx?id=56605)

::: moniker-end

::: moniker range="sc-orch-2022"

- [Download the pack for 2022](https://www.microsoft.com/download/details.aspx?id=104338)

::: moniker-end

## Registering and deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to runbook servers and Runbook Designer. For specific procedures, see [How To Install an Integration Pack](how-to-add-an-integration-pack.md).

## Configuring the Configuration Manager Integration Pack connection settings

Connections provide a way for you to define the way that the Configuration Manager Activities will connect to the Configuration Manager server(s) in your infrastructure. You must define at least one connection in order to use the Configuration Manager activities, but you can define as many as you need in order to connect to different Configuration Manager servers or utilize different connection settings or credentials.

### To set up a Configuration Manager connection

1.  In the Runbook Designer, select **Options**, and select **Configuration Manager**. The **Configuration Manager** dialog appears.

2.  On the **Connections** tab, select **Add** to begin the connection setup. The **Add Connection** dialog appears.

3.  In the **Name** box, enter a name for the connection. This could be the name of the *Active Directory* domain, or a descriptive name to distinguish the type of connection.

4.  In the Server box, enter the name or IP address of the Configuration Manager computer. If you're using the computer name, you can enter the NetBIOS name or the fully qualified domain name (FQDN). If you've installed Orchestrator on the Configuration Manager server, you can enter “Localhost” or the NetBIOS name of the server.

5.  In the **Username** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the Configuration Manager Site Server. 

> [!NOTE]
> The Username includes the domain name, for example: “contoso\admin”.

6.  Select **Test Connection**. When the message "Successfully connected" appears, select **OK**.

7. Select **OK** to close the configuration dialog, and select **Finish**.
