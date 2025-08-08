---
title: HP Operations Manager Integration Pack for System Center - Orchestrator
description: The Integration Pack for HP Operations Manager is an add-on for System Center - Orchestrator that enables you to automate the consolidation and correlation of fault and performance events across your entire physical and virtual IT infrastructure.
ms.custom: na
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: fbb368f4-4512-4960-a98d-66e36ee49d29
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---

# HP Operations Manager Integration Pack for System Center - Orchestrator


::: moniker range="sc-orch-2019"

>[!NOTE]
>HP Operations Manager Integration pack has been discontinued from System Center Orchestator 2022 and later.

::: moniker-end

The Integration Pack for HP Operations Manager is an add-on for System Center - Orchestrator that enables you to automate the consolidation and correlation of fault and performance events across your entire physical and virtual IT infrastructure.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information, see the [Privacy Statement for System Center - Orchestrator](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

The Integration Pack for HP Operations Manager requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and the HP Operations Manager application, see the respective product documentation.

::: moniker range="<=sc-orch-2019"
-  System Center 2016 integration packs require System Center 2016 - Orchestrator
-  System Center 2019 integration packs require System Center 2019 - Orchestrator
-  HP Operations Manager 9.x
::: moniker-end

## Download the Integration Pack

::: moniker range="<=sc-orch-2019"
- To download this integration pack for Orchestrator 2016, see [HP Operations Manager Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=54102).

- To download this integration pack for Orchestrator 2019, see [HP Operations Manager Integration Pack for System Center 2019 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=58108&WT.mc_id=rss_alldownloads_all).
::: moniker-end

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Add an Integration Pack](how-to-add-an-integration-pack.md).

## Configure the HP Operations Manager Connections

A connection establishes a reusable link between Orchestrator and an HP Operations Manager server. You can create as many connections as you require to specify links to multiple servers running HP Operations Manager. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

### Set up an HP Operations Manager configuration

1. In the Runbook Designer, select the **Options** menu, and select **HP Operations Manager**. The HP Operations Manager dialog appears.
2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.
3. In the **Name** box, enter a name for the connection. This could be the name of the HP Operations Manager server or a descriptive name to distinguish the type of connection.
4. Select the ellipsis button **(...)** next to the Type field and then select **HPOM Configuration**.
5. In the **HPOM Host** box, enter the name or IP address of the HP Operations Manager computer. If you're using the computer name, you can enter the NetBIOS name or the fully qualified domain name (FQDN).
6. In the **HPOM Port** box, enter the port used to connect to the HP Operations Manager computer. By default the **HPOM Port** is set to 443.
7. In the **HPOM Username** and **HPOM Password** boxes, enter the credentials that Orchestrator will use to connect to the HP Operations Manager server. When a connection is used for a **Launch Tool** activity, an HPOM Administrator account must be used. All other activities can use an HPOM User account.
8. Select **OK** to close the configuration dialog.
9. Add additional connections if applicable.
10. Select **Finish**.
