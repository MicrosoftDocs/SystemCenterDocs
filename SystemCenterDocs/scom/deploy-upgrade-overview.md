---
ms.assetid: 9d47d9ef-9a95-4b05-817f-75b3039f6e2c
title: Upgrade System Center Operations Manager
description: This guide provides information on how to upgrade to Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy23, UpdateFrequency.5, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade System Center Operations Manager

::: moniker range="sc-om-2025"

[!INCLUDE [discontinue-spf-2025.md](../includes/discontinue-spf-2025.md)]

This section of the Deployment Guide provides information about how to upgrade to System Center 2025 from an older supported version. You can upgrade to Operations Manager 2025 from Operations Manager versions 2022.

It's assumed in this guide that you're performing an upgrade from System Center 2022.

::: moniker-end

::: moniker range="sc-om-2022"

This section of the Deployment Guide provides information about how to upgrade to System Center 2022 from an older supported version. You can upgrade to Operations Manager 2022 from Operations Manager versions 2019.

It's assumed in this guide that you're performing an upgrade from System Center 2019.

>[!Note]
>If you upgrade from System Center Operation Manager 2019 UR3 or earlier, ensure to remove the duplicate management pack aliases. For more information on how to remove the management pack aliases, see [Remove duplicate Management pack aliases](/troubleshoot/system-center/scom/remove-duplicate-management-pack-aliases).

For information about installing Operations Manager on a computer where no previous version of Operations Manager exists, see Deploying System Center Operations Manager.

::: moniker-end

::: moniker range="sc-om-2019"

This section of the Deployment Guide provides information about how to upgrade to System Center 2019 from an older supported version. You can upgrade to Operations Manager 2019 from Operations Manager versions 2016.

It's assumed in this guide that you're performing an upgrade from System Center 2016. For information about installing Operations Manager on a computer where no previous version of Operations Manager exists, see [Deploying System Center Operations Manager](deploy-overview.md).

::: moniker-end

::: moniker range=">=sc-om-2019"

> [!NOTE]
> If your Operations Manager management group is integrated with Microsoft Azure Log Analytics (Formerly referred to as Microsoft Operations Management Suite (OMS)), its configuration will be retained and continue to function normally after the upgrade is complete.  

> [!WARNING]
> If you're upgrading two or more System Center components, you should review the upgrade process for each component.
>  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The following list are the affected System Center components integrated with Operations Manager and the recommended upgrade sequence:
>
> 1. Orchestrator - if you've the Operations Manager integration pack installed to support runbooks that perform automation against your Operations Manager management group.
> 2. Service Manager - if you configured the connectors to import alert and configuration item data of objects discovered and monitored from Operations Manager.
> 3. Data Protection Manager - if you've configured the central console to centrally manage your DPM environment.
   > 4. Operations Manager
   > 5. Virtual Machine Manager - if you've configured integration with Operations Manager to monitor the health of your VMM components, the virtual machines, and virtual machine hosts.

Before you upgrade to System Center Operations Manager, you must first determine whether all servers in your Operations Manager management group meet the minimum supported configurations. For more information, see [System Requirements: System Center Operations Manager](./system-requirements.md).

::: moniker-end

::: moniker range=">=sc-om-2019"

There are several options for upgrade:

1. If you run upgrade on a single-server management group, you only need to run the upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation won't continue until you resolve all issues.

2. If you're upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting and Audit Collection Services (ACS). You must also perform many pre-upgrade and post-upgrade tasks.

::: moniker-end

::: moniker range="sc-om-2019"

3. If you want to maintain your earlier version of Operations Manager (2016) environment, you can install version 2019 in parallel, upgrade your agents, and multi-home them between both management groups.  

::: moniker-end

::: moniker range="sc-om-2022"

3. If you want to maintain your earlier version of Operations Manager (2019) Operations Manager environment, you can install version 2022 in parallel, upgrade your agents, and multi-home them between both management groups.

::: moniker-end

::: moniker range="sc-om-2025"

3. If you want to maintain your earlier version of Operations Manager (2022) Operations Manager environment, you can install version 2025 in parallel, upgrade your agents, and multi-home them between both management groups.

::: moniker-end


::: moniker range="sc-om-2019"

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2019 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2016 RTM to the latest update rollup| Yes|

## In-place upgrade

System Center 2019 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2016

::: moniker-end

::: moniker range="sc-om-2022"

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2022 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
| Operations Manager 2019 RTM to the latest update| Yes|

## In-place upgrade
System Center 2022 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2019

> [!TIP]
> Although it is possible to upgrade from 2019 RTM directly to 2022, it's highly recommended to be on Update Rollup 3 or higher before upgrading.

::: moniker-end

::: moniker range="sc-om-2025"

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2025 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2022 RTM to the latest update| Yes|

## In-place upgrade

System Center 2025 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2022

::: moniker-end


::: moniker range=">=sc-om-2019"

## High level overview of upgrade steps for a distributed management group

The following steps outline the process for upgrading a distributed management group:

1. Accomplish [Pre-Upgrade Tasks](deploy-upgrade-pretasks.md)

2. Upgrade the initial management server and then additional management servers (each management server must be upgraded)

3. Upgrade ACS (because the ACS server must be on the same machine as a management server, we recommend you perform this step along with the upgrade of the management server on which ACS resides.)

4. \*Upgrade Gateway(s)

5. Upgrade Console

6. Push install to agent(s)/upgrade manually installed agents

7. Upgrade Web Console

8. Upgrade Reporting Server

9. Perform [Post-Upgrade Tasks](deploy-upgrade-post-tasks.md)

\*Steps 4 through 8 can be performed in parallel after all management servers have been upgraded.

::: moniker-end

::: moniker range="sc-om-2019"

## High level overview of upgrading agents and running two environments

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center supported version environment is left intact. Agents that have been upgraded to System Center 2019 Operations Manager on your upgrade path are fully capable of working with native Operations Manager 2016 functionality.  

Agents can be upgraded before the new Operations Manager management group is deployed and then configured to multi-home between the original management group and the new management group using your existing automation solution, or they can be upgraded after by discovering and performing a push-install from the new Operations Manager management group. For more information, see [How to Upgrade Agents in a Parallel Deployment](deploy-upgrade-agents-parallel.md).

::: moniker-end

::: moniker range="sc-om-2022"

## High level overview of upgrading agents and running two environments

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center supported version environment is left intact. Agents that have been upgraded to System Center 2022 Operations Manager on your upgrade path are fully capable of working with native Operations Manager 2019 functionality.

Agents can be upgraded before the new Operations Manager management group is deployed and then configured to multi-home between the original management group and the new management group using your existing automation solution, or they can be upgraded after by discovering and performing a push-install from the new Operations Manager management group. For more information, see [How to Upgrade Agents in a Parallel Deployment](deploy-upgrade-agents-parallel.md#upgrade-agents-in-a-parallel-deployment).

::: moniker-end

::: moniker range="sc-om-2025"

## High level overview of upgrading agents and running two environments

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center supported version environment is left intact. Agents that have been upgraded to System Center 2025 Operations Manager on your upgrade path are fully capable of working with native Operations Manager 2022 functionality.

Agents can be upgraded before the new Operations Manager management group is deployed and then configured to multi-home between the original management group and the new management group using your existing automation solution, or they can be upgraded after by discovering and performing a push-install from the new Operations Manager management group. For more information, see [How to Upgrade Agents in a Parallel Deployment](deploy-upgrade-agents-parallel.md#upgrade-agents-in-a-parallel-deployment).

::: moniker-end


::: moniker range=">=sc-om-2019"

1. Retain the original System Center Operations Manager environment.

2. Set up a new System Center Operations Manager environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, Operations console, Web console, and Reporting server.

3. Upgrade the System Center Operations Manager agents in your original management group to the same version of the new management group using either one of the following options:

    a. Push-Install option

    b. Manual/Command-line option

## Next Steps

- To understand the pre-upgrade tasks you should perform to complete the upgrade to your management group, see [Pre-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-pretasks.md).

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

::: moniker-end

::: moniker range="sc-om-2016"

This section of the Deployment Guide provides information about how to upgrade to System Center 2016 - Operations Manager or version 2019 from an older supported version.

It's assumed in this guide that you're performing an upgrade to System Center 2016 -  Operations Manager or version 2019. For information about installing Operations Manager on a computer where no previous version of Operations Manager exists, see [Deploying System Center Operations Manager](deploy-overview.md).

> [!NOTE]
> If your Operations Manager 2012 R2 or Operations Manager 2016 management group is integrated with Microsoft Azure Log Analytics (Formerly referred to as Microsoft Operations Management Suite (OMS)), its configuration will be retained and will continue to function normally after the upgrade is complete.  

> [!WARNING]
> If you're upgrading two or more System Center components, you should review the upgrade process for each component.
>  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The following list are the affected System Center components integrated with Operations Manager and the recommended upgrade sequence:
>
> 1. Orchestrator - if you've the Operations Manager integration pack installed to support runbooks that perform automation against your Operations Manager management group.
> 2. Service Manager - if you configured the connectors to import alert and configuration item data of objects discovered and monitored from Operations Manager.
> 3. Data Protection Manager - if you've configured the central console to centrally manage your DPM environment.
   > 4. Operations Manager
   > 5. Virtual Machine Manager - if you've configured integration with Operations Manager to monitor the health of your VMM components, the virtual machines, and virtual machine hosts.

Before you upgrade to System Center Operations Manager, you must first determine whether all the servers in your Operations Manager management group meet the minimum supported configurations. For more information, see [System Requirements: System Center Operations Manager](./system-requirements.md).

There are several options for upgrade:

1. If you run upgrade on a single-server management group, you only need to run upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation won't continue until you resolve all issues.

2. If you're upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting, and Audit Collection Services (ACS). You must also perform a number of pre-upgrade and post-upgrade tasks.

3. If you want to maintain your Operations Manager 2012 R2 or System Center 2016 - Operations Manager environment, you can install version 2019 in parallel, upgrade your agents and multi-home them between both management groups.  

4. If you want to maintain your Operations Manager 2012 R2 environment, you can install System Center 2016 - Operations Manager in parallel, upgrade your agents, and multi-home them between both management groups.  

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2016 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2012 R2 | Yes

The following table lists the scenarios in which coexistence between Operations Manager 2019 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2016 RTM to the latest update rollup| Yes|
|  Operations Manager 2012 R2 to the latest update rollup| Yes|

## In-place upgrade

System Center 2016 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2016 Technical Preview 5 - Operations Manager
- System Center 2012 R2 Operations Manager with Update Rollup 12

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

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center 2012 R2 Operations Manager or Operations Manager 2016 environment is left intact. Agents that have been upgraded to System Center 2016 Operations Manager depending on your upgrade path are fully capable of working with native System Center 2012 R2 Operations Manager or Operations Manager 2016 functionality.  

Agents can be upgraded before the new Operations Manager management group is deployed and then configured to multi-home between the original management group and the new management group using your existing automation solution, or they can be upgraded after by discovering and performing a push-install from the new Operations Manager management group. For more information, see [How to Upgrade Agents in a Parallel Deployment](deploy-upgrade-agents-parallel.md).  

1. Retain the original System Center 2012 R2 Operations Manager or Operations Manager 2016 environment.

2. Set up a new System Center Operations Manager environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, Operations console, Web console, and Reporting server.

3. Upgrade the System Center Operations Manager agents in your original management group to the same version of the new management group using either one of the following options:

    a. Push-Install option

    b. Manual/Command-line option

## Next Steps

- To understand the pre-upgrade tasks you should perform to complete the upgrade to your management group, see [Pre-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-pretasks.md).

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

::: moniker-end
