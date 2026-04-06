---
title: Configuration Manager Integration Pack
description: The Integration Pack for Configuration Manager is an add-on for System Center - Orchestrator that enables you to automate common Configuration Manager functions.
ms.custom: na
ms.date: 05/28/2025
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 4d2feb46-3f4c-4ed6-adbf-50097f94ea61
author: Jeronika-MS
ms.update-cycle: 1095-days
ms.author: v-gajeronika
---
# Configuration Manager Integration Pack for System Center - Orchestrator

The Integration Pack for Configuration Manager is an add-on for System Center - Orchestrator that enables you to automate common Configuration Manager management functions. In this article, you'll learn about Integration Pack for Configuration Manager.

With this integration pack, you can also create workflows that interact with and transfer information to the integration packs for System Center Service Manager, System Center Data Protection Manager, System Center Operations Manager, and System Center Virtual Machine Manager.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more Orchestrator-related privacy information, see the [Privacy Statement for System Center - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System requirements

Before you can install the Integration Pack for Configuration Manager, you must first install and configure the following listed software. For more information about how to install and configure Orchestrator and Active Directory, see the respective product documentation.

System Center integration packs require System Center - Orchestrator and Configuration Manager.

## Download the integration pack

::: moniker range="<=sc-orch-2019"

- [Download the pack for 2016](https://www.microsoft.com/en-us/download/details.aspx?id=54098)

::: moniker-end

::: moniker range="sc-orch-2022"

- [Download the pack for 2022](https://www.microsoft.com/download/details.aspx?id=104338)

::: moniker-end

::: moniker range="sc-orch-2025"

Configuration Manager Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the Configuration Manager integration pack [here](https://www.microsoft.com/download/details.aspx?id=104338).

::: moniker-end

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to runbook servers and Runbook Designer. For specific procedures, see [How To install an integration pack](how-to-add-an-integration-pack.md).

## Configure the Configuration Manager integration pack connection settings

Connections provide a way for you to define the way that the Configuration Manager Activities will connect to the Configuration Manager server(s) in your infrastructure. You must define at least one connection in order to use the Configuration Manager activities, but you can define as many as you need in order to connect to different Configuration Manager servers or utilize different connection settings or credentials.

### Set up a Configuration Manager connection

To set up a Configuration Manager connection, follow these steps:

1. In the Runbook Designer, select **Options**, and select **Configuration Manager**. The **Configuration Manager** dialog appears.

2. On the **Connections** tab, select **Add** to begin the connection setup. The **Add Connection** dialog appears.

3. In the **Name** box, enter a name for the connection. This could be the name of the *Active Directory* domain, or a descriptive name to distinguish the type of connection.

4. In the Server box, enter the name or IP address of the Configuration Manager computer. If you're using the computer name, you can enter the NetBIOS name or the Fully Qualified Domain Name (FQDN). If you've installed Orchestrator on the Configuration Manager server, you can enter “Localhost” or the NetBIOS name of the server.

5. In the **Username** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the Configuration Manager Site Server. 

> [!NOTE]
> The Username includes the domain name, for example: “contoso\admin”.

6. Select **Test Connection**. When the message "Successfully connected" appears, select **OK**.

7. Select **OK** to close the configuration dialog, and select **Finish**.
