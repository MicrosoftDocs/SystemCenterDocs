---
title: System Center integration pack for System Center - Service Manager
description: The article describes the integration pack for System Center - Service Manager. The pack is an add-in for System Center - Orchestrator.
ms.date: 04/04/2019
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# Integration pack for System Center - Service Manager

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The integration pack for System Center - Service Manager is an add-in for System Center - Orchestrator. It enables you to use Service Manager to coordinate and use operational data in an existing IT environment comprised of service desk systems, configuration management systems, and event monitoring systems.

[Learn more](https://go.microsoft.com/fwlink/?LinkID=275796) about integration packs.

## System requirements

The Service Manager integration pack requires the following software to be installed and configured before you implement the integration:

-   System Center - Orchestrator
-   System Center - Service Manager
-   The Service Manager integration pack is only supported for use on computers set to use:
    -   The ENU Locale
    -   The U.S. English date format (month/day/year)


## Download the pack

- [Download the pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [Download the pack for 1801](https://www.microsoft.com/download/details.aspx?id=56605)
- [Download the pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)

## Register and deploy the pPack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. [Learn more](how-to-add-an-integration-pack.md) about installing an integration pack.

## Configure the connections

A connection establishes a reusable link between Orchestrator and a Service Manager Server. You can create as many connections as you need to specify links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.


1.  In the Runbook Designer, click the **Options** menu, and select Service Manager.
2.  On the **Connections** tab, click **Add** to begin the connection setup.
3.  In the **Name** box, enter a name for the connection. This could be the name of the Service Manager server, or a descriptive name to distinguish the type of connection.
4.  In the **Server** box, click the ellipsis button **(...)**. Select the Service Manager server, and then click **OK**.
5.  In the **Credentials** section, type the **Domain**, **User name**, and **Password** that the Orchestrator server will use to connect to the Service Manager computer.
6.  In the **Monitoring Intervals** section, enter the **Polling** and **Reconnect** intervals that the Orchestrator server will use with the connection to the Server Manager computer. The default is **10 seconds**.
7.  Click **Test Connection**. When the success message appears, click **OK**.
8.  Add additional connections if applicable. Click **OK** to close the configuration dialog box, and then click **Finish**.
