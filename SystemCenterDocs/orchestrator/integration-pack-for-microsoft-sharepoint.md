---
title: System Center integration pack for SharePoint
description: This article describes the SharePoint integration pack for System Center - Orchestrator.
ms.date: 04/04/2019
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# Integration pack for SharePoint

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

Integration packs are add-ons for System Center - Orchestrator. They help you to optimize IT operations across heterogeneous environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and by non-Microsoft products.

The System Center Integration Pack for Microsoft SharePoint enables the automation of common tasks in SharePoint, for example, to create list items, to upload and download documents, and to monitor a list for changes.

[Learn more](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx) about Orchestrator privacy.


## System Requirements

The integration pack for SharePoint requires the following software to be installed and configured before you implement the integration.

-   System Center - Orchestrator
-   Microsoft .NET Framework 4
-   Microsoft SharePoint

## Download the pack

- [Download the pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [Download the pack for 1801](https://www.microsoft.com/download/details.aspx?id=56605)
- [Download the pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. Learn about [installing the pack](how-to-add-an-integration-pack.md).

## Configure the pack connections

A connection establishes a reusable link between Orchestrator and a SharePoint site. You can create as many connections as you require to specify links to multiple sites. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.


1.  In the **Orchestrator Runbook Designer**, click **Options**, and then click **Microsoft SharePoint.** The **Microsoft SharePoint** dialog box appears.
2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.
3.  In the **Name** box, enter a name for the connection. This name can be the name of the SharePoint site or a descriptive name to distinguish the type of connection.
4.  In the **Type** box, select **SharePoint Configuration.**
5.  In the **SharePoint Site** box, enter the URL of the SharePoint site that you want to integrate with.
6.  In the **User Name** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the SharePoint site.
7.  In the **Domain** box, enter the name of the domain to authorize access.
8.  In the **SharePoint Online** box, enter **False**.
9.  In the **Default Monitor Interval (seconds)** box, enter a time-out value, in seconds, or keep the default value.

10. In the **Default Maximum Items** box, enter a maximum value, or keep the default value.
11. Click **OK**.
12. Add additional connections, if applicable, and then click **Finish**.
