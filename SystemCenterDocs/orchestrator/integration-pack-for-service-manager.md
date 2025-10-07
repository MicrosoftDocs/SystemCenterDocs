---
title: System Center integration pack for System Center - Service Manager
description: The article describes the integration pack for System Center - Service Manager. The pack is an add-in for System Center - Orchestrator.
ms.date: 11/19/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
---

# Integration pack for System Center - Service Manager

The integration pack for System Center - Service Manager is an add-in for System Center - Orchestrator. It enables you to use Service Manager to coordinate and use operational data in an existing IT environment comprised of service desk systems, configuration management systems, and event monitoring systems.

[Learn more](https://go.microsoft.com/fwlink/?LinkID=275796) about integration packs.

## System requirements

The Service Manager integration pack requires the following software to be installed and configured before you implement the integration:

- System Center - Orchestrator
- System Center - Service Manager
- The Service Manager integration pack is only supported for use on computers set to use:
    - The ENU Locale
    - The U.S. English date format (month/day/year)

>[!Note]
>- SCO's SCSM IP must be deployed on machines that already have `Microsoft.EnterpriseManagement.Core.dll`.
>- Ensure to install the Service Manager console on the machine where the IP is deployed as DLL is removed from the 2022 SCSM IP.

## Download the pack

::: moniker range="sc-orch-2025"

Service Manager Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the Integration Pack for Service Manager [here](https://www.microsoft.com/download/details.aspx?id=104341).

::: moniker-end

::: moniker range="sc-orch-2022"

- [Download the pack for 2022](https://www.microsoft.com/download/details.aspx?id=104341)

::: moniker-end

::: moniker range="<=sc-orch-2019"
- [Download the pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [Download the pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)
::: moniker-end

## Register and deploy the pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. [Learn more](how-to-add-an-integration-pack.md) about installing an integration pack.

## Configure the connections

A connection establishes a reusable link between Orchestrator and a Service Manager Server. You can create as many connections as you need to specify links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

1. In the Runbook Designer, select the **Options** menu, and select Service Manager.
2. On the **Connections** tab, select **Add** to begin the connection setup.
3. In the **Name** box, enter a name for the connection. This could be the name of the Service Manager server or a descriptive name to distinguish the type of connection.
4. In the **Server** box, select the ellipsis button **(...)**. Select the Service Manager server, and select **OK**.
5. In the **Credentials** section, enter the **Domain**, **User name**, and **Password** that the Orchestrator server will use to connect to the Service Manager computer.
6. In the **Monitoring Intervals** section, enter the **Polling** and **Reconnect** intervals that the Orchestrator server will use with the connection to the Server Manager computer. The default is **10 seconds**.
7. Select **Test Connection**. When the success message appears, select **OK**.
8. Add additional connections if applicable. Select **OK** to close the configuration dialog, and select **Finish**.
