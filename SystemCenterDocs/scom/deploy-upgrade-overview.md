---
ms.assetid: 9d47d9ef-9a95-4b05-817f-75b3039f6e2c
title: Upgrading System Center Operations Manager
description: This guide provides information on how to upgrade to Operations Manager.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 03/14/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2016 <sc-om-1807 || sc-om-2019'
---

# Upgrading System Center Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

::: moniker range="sc-om-2019"

This section of the Deployment Guide provides information about how to upgrade to System Center 2019 from an older supported version. You can upgrade to Operations Manager 2019 from Operations Manager versions 2016, 1801 or 1807.

It is assumed in this guide that you are performing an upgrade from System Center 2016, 1801, or 1807. For information about installing Operations Manager on a computer where no previous version of Operations Manager exists, see [Deploying System Center Operations Manager](deploy-overview.md).

> [!NOTE]
> If your Operations Manager management group is integrated with Microsoft Azure Log Analytics (Formerly referred to as Microsoft Operations Management Suite (OMS)), its configuration will be retained and continue to function normally after the upgrade is complete.  

> [!WARNING]
> If you are upgrading two or more System Center components, you should review the upgrade process for each component.
>  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The following list are the affected System Center components integrated with Operations Manager and the recommended upgrade sequence:
>
   > 1. Orchestrator - if you have the Operations Manager integration pack installed to support runbooks that perform automation against your Operations Manager management group.
   > 2. Service Manager - if you configured the connectors to import alert and configuration item data of objects discovered and monitored from Operations Manager.
   > 3. Data Protection Manager - if you have configured the central console to centrally manage your DPM environment.
   > 4. Operations Manager
   > 5. Virtual Machine Manager - if you have configured integration with Operations Manager to monitor the health of your VMM components, the virtual machines and virtual machine hosts.

Before you upgrade to System Center Operations Manager, you must first determine whether all servers in your Operations Manager management group meet the minimum supported configurations. For more information, see [System Requirements: System Center Operations Manager](plan-system-requirements.md).

There are several options for upgrade:

1. If you run upgrade on a single-server management group, you only need to run the upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation will not continue until you resolve all issues.

2. If you are upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting and Audit Collection Services (ACS). You must also perform a number of pre-upgrade and post-upgrade tasks.

3. If you want to maintain your earlier version of Operations Manager (2016, 1801, 1807) Operations Manager environment, you can install version 2019 in parallel, upgrade your agents and multi-home them between both management groups.  

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2019 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2016 RTM to the latest update rollup| Yes|
|  Operations Manager 1801 and 1807| Yes|

## In-place upgrade

System Center 2019 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2016
- System Center 1801
- System Center 1807

## High level overview of upgrade steps for a distributed management group

The following steps outline the process for upgrading a distributed management group:

1. Accomplish [Pre-Upgrade Tasks](deploy-upgrade-pretasks.md)

2. Upgrade the initial management server and then additional management servers (each management server must be upgraded)

3. Upgrade ACS (because the ACS server must be on same machine as a management server, we recommend you perform this step along with the upgrade of the management server on which ACS resides.)

4. \*Upgrade Gateway(s)

5. Upgrade Console

6. Push install to agent(s) / upgrade manually installed agents

7. Upgrade Web Console

8. Upgrade Reporting Server

9. Perform [Post-Upgrade Tasks](deploy-upgrade-post-tasks.md)

\*Steps 4 through 8 can be performed in parallel after all management servers have been upgraded.


## High level overview of upgrading agents and running two environments

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center supported version environment is left intact. Agents that have been upgraded to System Center 2019 Operations Manager on your upgrade path, are fully capable of working with native Operations Manager 2016, 1801 and 1807 functionality.  

Agents can be upgraded before the new Operations Manager management group is deployed and then configured to multi-home between the original management group and the new management group using your existing automation solution, or they can be upgraded after by discovering and performing a push-install from the new Operations Manager management group.  For further information, see [How to Upgrade Agents in a Parallel Deployment](deploy-upgrade-agents-parallel.md).  

1. Retain the original System Center Operations Manager environment.

2. Set up a new System Center Operations Manager environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, Operations console, Web console, and Reporting server.

3. Upgrade the System Center Operations Manager agents in your original management group to the same version of the new management group using either one of the following options:

    a. Push-Install option

    b. Manual / Command-line option

## Next steps

- To understand the pre-upgrade tasks you should perform to complete the upgrade to your management group, see [Pre-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-pretasks.md).

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

::: moniker-end

::: moniker range="<=sc-om-1807"

This section of the Deployment Guide provides information about how to upgrade to System Center 2016 - Operations Manager or version 1801 from an older supported version.

It is assumed in this guide that you are performing an upgrade to System Center 2016 -  Operations Manager or version 1801. For information about installing Operations Manager on a computer where no previous version of Operations Manager exists, see [Deploying System Center Operations Manager](deploy-overview.md).

> [!NOTE]
> If your Operations Manager 2012 R2 or Operations Manager 2016 management group is integrated with Microsoft Azure Log Analytics (Formerly referred to as Microsoft Operations Management Suite (OMS)), its configuration will be retained and continue to function normally after the upgrade is complete.  

> [!WARNING]
> If you are upgrading two or more System Center components, you should review the upgrade process for each component.
>  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The following list are the affected System Center components integrated with Operations Manager and the recommended upgrade sequence:
>
   > 1. Orchestrator - if you have the Operations Manager integration pack installed to support runbooks that perform automation against your Operations Manager management group.
   > 2. Service Manager - if you configured the connectors to import alert and configuration item data of objects discovered and monitored from Operations Manager.
   > 3. Data Protection Manager - if you have configured the central console to centrally manage your DPM environment.
   > 4. Operations Manager
   > 5. Virtual Machine Manager - if you have configured integration with Operations Manager to monitor the health of your VMM components, the virtual machines and virtual machine hosts.

Before you upgrade to System Center Operations Manager, you must first determine whether all servers in your Operations Manager management group meet the minimum supported configurations. For more information, see [System Requirements: System Center Operations Manager](plan-system-requirements.md).

There are several options for upgrade:

1. If you run upgrade on a single-server management group, you only need to run upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation will not continue until you resolve all issues.

2. If you are upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting and Audit Collection Services (ACS). You must also perform a number of pre-upgrade and post-upgrade tasks.

3. If you want to maintain your Operations Manager 2012 R2 or System Center 2016 - Operations Manager environment, you can install version 1801 in parallel, upgrade your agents and multi-home them between both management groups.  

4. If you want to maintain your Operations Manager 2012 R2 environment you can install System Center 2016 - Operations Manager in parallel, upgrade your agents and multi-home them between both management groups.  

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2016 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2012 R2 | Yes

The following table lists the scenarios in which coexistence between Operations Manager 1801 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2016 RTM to the latest update rollup| Yes|
|  Operations Manager 2012 R2 to the latest update rollup| Yes|

## In-place upgrade

System Center 2016 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2016 Technical Preview 5 - Operations Manager
- System Center 2012 R2 Operations Manager with Update Rollup 12

System Center Operations Manager 1801 supports an in-place upgrade from the following versions:

- System Center 2012 R2 UR12 to the latest update rollup  
- System Center 2016 RTM to the latest update rollup  

## High level overview of upgrade steps for a distributed management group

The following steps outline the process for upgrading a distributed management group:

1. Accomplish [Pre-Upgrade Tasks](deploy-upgrade-pretasks.md)

2. Upgrade the initial management server and then additional management servers (each management server must be upgraded)

3. Upgrade ACS (because the ACS server must be on same machine as a management server, we recommend you perform this step along with the upgrade of the management server on which ACS resides.)

4. \*Upgrade Gateway(s)

5. Upgrade Console

6. Push install to agent(s) / upgrade manually installed agents

7. Upgrade Web Console

8. Upgrade Reporting Server

9. Perform [Post-Upgrade Tasks](deploy-upgrade-post-tasks.md)

\*Steps 4 through 8 can be performed in parallel after all management servers have been upgraded.


## High level overview of upgrading agents and running two environments

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center 2012 R2 Operations Manager or Operations Manager 2016 environment is left intact. Agents that have been upgraded to System Center 2016 Operations Manager or version 1801 depending on your upgrade path, are fully capable of working with native System Center 2012 R2 Operations Manager or Operations Manager 2016 functionality.  

Agents can be upgraded before the new Operations Manager management group is deployed and then configured to multi-home between the original management group and the new management group using your existing automation solution, or they can be upgraded after by discovering and performing a push-install from the new Operations Manager management group. For more information, see [How to Upgrade Agents in a Parallel Deployment](deploy-upgrade-agents-parallel.md).  

1. Retain the original System Center 2012 R2 Operations Manager or Operations Manager 2016 environment.

2. Set up a new System Center Operations Manager environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, Operations console, Web console, and Reporting server.

3. Upgrade the System Center Operations Manager agents in your original management group to the same version of the new management group using either one of the following options:

    a. Push-Install option

    b. Manual / Command-line option

## Next steps

- To understand the pre-upgrade tasks you should perform to complete the upgrade to your management group, see [Pre-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-pretasks.md).

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

::: moniker-end
