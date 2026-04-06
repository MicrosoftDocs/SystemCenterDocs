---
ms.assetid: 90bd75e0-de7a-4ca4-ae7e-681a9eb21aba
title: Integrate VMM with Operations Manager for monitoring and reporting
description: This article describes how to integrate VMM with Operations Manager for monitoring and reporting
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 05/15/2025
ms.topic: how-to
ms.service: system-center
ms.update-cycle: 180-days
ms.subservice: virtual-machine-manager
ms.custom: engagement-fy23, engagement-fy24
---


# Integrate VMM with Operations Manager for monitoring and reporting



This article describes how to integrate System Center Virtual Machine Manager (VMM) with System Center Operations Manager to monitor the health of virtualization hosts, virtual machines, and other resources in the VMM compute fabric.

- Operations Manager monitors the VMM server and all the hosts and virtual machines in the VMM fabric.
- An Operations Manager management group can monitor multiple VMM instances. The VMM fabric can only be monitored by a single Operations Manager management group.
- The Fabric Health Dashboard is imported to Operations Manager with the VMM management packs. It shows a detailed overview of the health of the VMM fabric and private clouds. You can link to other dashboards to drill into network and storage monitoring.

## Deployment summary

You set up Operations Manager with VMM as follows:

1. Ensure the [prerequisites](../scom/system-requirements.md) are met.
2. Install the Operations Manager console on the VMM server so that you can monitor VMM from the server.
3. Install Operations Manager agents on the VMM management server and all hosts under management by VMM.
4. Locate the latest management pack.
5. Run the integration wizard to integrate VMM and Operations Manager. The wizard does the following:

    - Imports the VMM management packs into the Operations Manager.
    - Optionally enables Performance and Resource Optimization (PRO). PRO information is provided by the Operations Manager, and can be mapped to VMM to optimize performance. You can map specific Operations Manager alerts to remedial actions in VMM. For example, you could migrate VMs to a different host after a hardware issue. In addition, with PRO enabled, Operations Manager can detect resource issues or hardware failures in the virtualization infrastructure.
    - Optionally enables maintenance mode. VMM can place hosts in maintenance mode for servicing. When a host is in maintenance mode, VMM uses live migration to move VMs to another location and doesn't place new VMs on the host. If the maintenance mode is enabled for Operations Manager monitoring, when a host is placed into maintenance mode in VMM, Operations Manager also places it in the same mode. In the maintenance mode, the Operations Manager agent suppresses alerts, notifications, and state changes, so that the host isn't monitored while regular hardware and software maintenance activities are in progress.
    - Enables support for SQL Server Analysis Services (SSAS) and the reporting capabilities provided by SSAS.


## Before you start


::: moniker range="sc-vmm-2016"

>[!NOTE]
> Ensure that you're using a supported version of Operations Manager (running on System Center 2016 or a later version).

::: moniker-end

::: moniker range="sc-vmm-2019"

>[!NOTE]
>Ensure that you're using a supported version of Operations Manager (running on System Center 2019 or a later version).

::: moniker-end

::: moniker range="sc-vmm-2022"

>[!NOTE]
>Ensure that you're using a supported version of Operations Manager (running on System Center 2022).

::: moniker-end

::: moniker range="sc-vmm-2025"

>[!NOTE]
>Ensure that you're using a supported version of Operations Manager (running on System Center 2025).

::: moniker-end

::: moniker range="<=sc-vmm-2019"
- Operations Manager must use SQL Server 2012 SP2, SQL Server 2014, or SQL Server 2016 with reporting services enabled. To use the forecasting reports, SQL Server Analysis Services must be installed on the Operations Manager reporting server. The SSAS instance name must match the SQL Server Reporting Services (MSSQLSERVER).
::: moniker-end

::: moniker range="sc-vmm-2022"
- Operations Manager must use SQL Server 2016, SQL Server 2017, SQL Server 2019, or SQL Server 2022 with reporting services enabled. To use the forecasting reports, SQL Server Analysis Services must be installed on the Operations Manager reporting server. The SSAS instance name must match the SQL Server Reporting Services (MSSQLSERVER).
::: moniker-end
::: moniker range="sc-vmm-2025"
- Operations Manager must use SQL Server 2019 or SQL Server 2022 with reporting services enabled. To use the forecasting reports, SQL Server Analysis Services must be installed on the Operations Manager reporting server. The SSAS instance name must match the SQL Server Reporting Services (MSSQLSERVER).
::: moniker-end
- The version of the Operations Manager operations console that is installed on the VMM management server must match the version of Operations Manager with which you intend to integrate. The Operations Manager agent version agent should be supported by the Operations Manager version.
- Ensure that the version of Windows PowerShell that's on all Operations Manager management servers is the most recent version supported by that version of Operations Manager. To determine which version of Windows PowerShell is on a server, run **Get-Host | Select-Object Version**
- Ensure that port 5724 is open between the VMM and Operations Manager servers.
- You need VMM admin permissions to run the integration wizard.
- VMM monitoring packs support up to 400 hosts, with up to 8000 virtual machines.

## Install the Operations Manager console

1. Run Operations Manager Setup on each VMM management server.
2. In the wizard, select the **Operations** Console to install it.

## Install the Operations Manager agent

1. Install the Operations Manager agent on each VMM server, and on each host managed in the VMM fabric.
2. You can install the agent from the Operations Manager Operations console, from Operations Manager setup, or from the command line. To understand the different methods for agent deployment, review the [Managing discovery and agents](../scom/manage-deploy-windows-agent-console.md) section in Operations Manager documentation.

## Locate the management packs

- The latest versions of management packs are coupled with every new release of VMM build.

- To locate the management packs, open the management packs folder on the VMM server. The default location is: \
  `C:\Program Files\Microsoft System Center\Virtual Machine Manager\ManagementPacks`.

## Run the integration wizard

Run the wizard to connect the VMM server to the Operations Manager server and import the VMM management pack to Operations Manager.

1.  In the VMM console, select **Settings** > **System Center Settings** > **Operations Manager Server** > **Properties**.

    > [!NOTE]
    > If the Operations Manager connection has already been established, selecting **Properties** opens the **Operation Manager Settings** dialog. If this dialog appears and doesn't describe the correct connection, remove the current connection before you enter the correct information.

2.  In **Introduction**, select **Next**.
3.  In **Connection to Operations Manager**, specify the Operations Manager server name, and select an account to use to connect to it. You can use the VMM server service account or specify a Run As account. This account must be a member of the Operations Manager Administrator role.
4.  Select **Enable Performance and Resource Optimization (PRO)** if necessary.
5.  Select **Enable maintenance mode integration with Operations Manager**, if desired. Select **Next**.

    When hosts are placed in maintenance mode using the VMM management server, Operations Manager places them in the maintenance mode as well. In this mode, the Operations Manager agent suppresses alerts, notifications, rules, monitors, automatic responses, state changes, and new alerts.

6.  Enter credentials for Operations Manager to connect with the VMM management server and select **Next**. This account will be added to the Administrator user role in VMM.
7. Review the information in the **Summary** page and select **Finish**. You can view the status of the new connection in the **Jobs** workspace.
8. With **System Center Settings** still selected, in the results pane, right-click **Operations Manager Server**, and select **Properties**. In **Operation Manager Settings** > **Details** > **Connection Status**, confirm that the connection is **OK**.

If you later remove a connection to an Operations Manager server, this doesn't remove the VMM management packs from the server, but the connector is removed.

## Monitor VMM in the Operations Manager console

You can monitor VMM processes and state in any of the VMM dashboards that appear in the Operations Manager console - the fabric dashboard, VM dashboard, or VMM host dashboard.

1. In the Operations console for Operations Manager, select **Monitoring**.
2. To monitor VMs, select **Virtual Machine Manager**. This dashboard includes health and performance information for virtual machines, hosts, and VMM servers.
3. To monitor VMM hosts, select **VMM Host Dashboard**. You can monitor the health of virtualization hosts discovered in the VMM fabric, and get information about the host properties, status, VMs, alerts, and performance.
4. To monitor a private cloud, select **Fabric Health Dashboard**. For each cloud, the dashboard monitors the state of host groups, the compute properties of the cloud (CPU, network adapters, and so on), and storage information such as pools, file share, LUNs, and network monitoring. You can scope the dashboard to physical or virtual resources or to a particular cloud tenant.
5. In **Virtual Machine Manager Views**, you can view graphic representations of managed systems. After you connect the VMM and Operation Manager servers for the first time, it can take several hours until the diagrams are available in the console.

## Next steps

- [Run VMM reports](monitor.md#report-with-operations-manager) in Operations Manager.
