---
description: Explains why you should use the Central Console to manage multiple DPM servers and how to install the console.
ms.topic: how-to
ms.service: system-center
keywords:
ms.date: 01/29/2026
title: Manage multiple DPM servers with Central Console
ms.subservice: data-protection-manager
ms.assetid: 6e08e911-36e0-48d6-b71e-df4741811a0a
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
---

# Manage multiple DPM servers with Central Console

Central Console is a System Center Operations Manager console that you can deploy to manage and monitor multiple System Center Data Protection Manager (DPM) servers from a single location. It provides:

- Centralized monitoring of DPM servers from a single location - You can monitor different versions of DPM and track the status of servers, tasks, protected resources, tape libraries, available storage, and disk space.

- Role-based access control

- Remote recovery
     and remote corrective actions

- Service level agreement (SLA)-based alerting and alert consolidation - Alerts are generated when an SLA is broken.
    You can consolidate alerts and work on high priority items as follows:

    - Repeated alerts - Display only one alert for repeated alerts. For example, if a job is scheduled to run hourly and hasn't run for the last 10 hours, only one alert for the failed job is displayed.

    - Same root cause - If multiple alerts have the same root cause or if multiple backups fail for the same data source, only the alert informing you of the failure is generated.

    - Ticket generation - If you're using a ticketing system, only one ticket is generated.

- Scoped console - This is based on the DPM Administrator Console with a few minor differences.

## Set up Central Console

::: moniker range="sc-dpm-2019"

You can install Central Console on a server computer running Windows Server 2008 R2 or later, or a client computer running Windows 7 or later. You can't install it on the DPM server. Set up Central Console by installing the relevant Operations Manager agent on each DPM server you want to manage. Then, install the Central Console on the Operations Manager server by importing the DPM management pack and then installing the console.

::: moniker-end

>[!NOTE]
>To upgrade the DPM central console to a latest version, uninstall the older version and then install the latest.

If upgrade isn't supported:

1.  Deploy an Operations Manager agent to your DPM server.  [Read more](./use-ops-manager-to-manage-monitor-dpm.md#BKMK_OM).

2. The Central Console consists of two management packs: `Microsoft.SystemCenter.DataProtectionManager.2012.Discovery.mp` and `Microsoft.SystemCenter.DataProtectionManager.2012.Library.mp`. You need to import both of these management packs. They're located in `<CDDrive:>\Management Packs`. When you import the management pack, Windows displays a warning about write actions. This warning is expected, and you can select **OK** to continue.

    > [!NOTE]
    > The Central Console requires the version of the management pack that's available in the DPM installation folder. However, after you install this version, you can update to the latest management pack version available on the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=56560).

3. After importing the pack, install the Central Console. To do this, in the Setup screen of Operations Manager, select **Install Central Console Server and Client-side Components** if you want to monitor DPM servers on which the Operations Manager agent is present and use the scoped DPM Administrator console.
    Select **Install Central Console** if you want to use the scoped DPM Administrator console only, without server monitoring.
    Select **Install Central Console Server-side Components** if you want to monitor servers only, without using the scoped DPM Administrator console.

4. DPM adds firewall exceptions for port 6075 and creates a default role-based access configuration.

5. After you install the Central Console, a view folder **System Central 2012 Data Protection Manager** is created in the Operations Manager console. You can manage most tasks for managed DPM servers from the Central Console.
