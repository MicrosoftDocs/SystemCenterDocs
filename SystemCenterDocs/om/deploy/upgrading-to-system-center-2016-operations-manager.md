---
title:  Upgrading to System Center 2016 - Operations Manager
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---


# Upgrading to System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager


This section of the Deployment Guide provides information about how to upgrade to System Center 2016 - Operations Manager from System Center Operations Manager 2012 R2.

> [!NOTE]
> This is the only supported upgrade path to System Center 2016 - Operations Manager. If you are using Operations Manager 2012 Service Pack 1 (SP1), you must first upgrade to System Center Operations Manager 2012 R2 with Update Rollup 9.

It is assumed in this guide that you are performing an upgrade to System Center 2016 -  Operations Manager. For information about installing Operations Manager on a computer where no previous version of Operations Manager exists, see [Deploying System Center 2016 - Operations Manager](deploying-system-center-2016-operations-manager.md).

> [!NOTE]
> If your Operations Manager 2012 R2 management group is integrated with Microsoft Operations Management Suite (OMS), its configuration will be retained and continue to function normally after the upgrade is complete.  

> [!WARNING]
> If you are upgrading two or more System Center components, you must follow the procedures that are documented in Upgrade Sequencing for System Center 2012 R2.
>  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:
   > 1. Configuration Manager
   > 2. Data Protection Manager
   > 3. Orchestrator
   > 4. Configuration Manager
   > 5. Virtual Machine Manager

Before you upgrade to System Center 2016 - Operations Manager, you must first determine whether all servers in your Operations Manager management group meet the minimum supported configurations. For more information, see [System Requirements: System Center 2016 - Operations Manager](../plan/system-requirements.md).

There are several options for upgrade:

1. If you run upgrade on a single-server management group, you only need to run upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation will not continue until you resolve all issues.

2. If you are upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting and Audit Collection Services (ACS). You must also perform a number of pre-upgrade and post-upgrade tasks.

3. If you want to maintain your Operations Manager 2012 R2 environment you can install System Center 2016 - Operations Manager in parallel, upgrade your agents and multi-home them between both management groups.

### High level overview of System Center 2016 Operations Manager upgrade steps for a distributed management group

The following steps outline the process for upgrading a distributed management group:

1. Accomplish [Pre-Upgrade Tasks](pre-upgrade-tasks-when-upgrading-to-system-center-2016-operations-manager.md)

2. Upgrade the initial management server and then additional management servers (each management server must be upgraded)

3. Upgrade ACS (because the ACS server must be on same machine as a management server, we recommend you perform this step along with the upgrade of the management server on which ACS resides.)

4. \*Upgrade Gateway(s)

5. Upgrade Console

6. Push Install to Agent(s) / Upgrading Manually Installed Agents

7. Upgrade Web Console

8. Upgrade Reporting Server

9. Perform [Post-Upgrade Tasks](post-upgrade-tasks-when-upgrading-to-system-center-2016-operations-manager.md)

\*Steps 4 through 8 can be performed in parallel after all management servers have been upgraded.


### High level overview System Center 2016 Operations Manager - upgrading 2012 R2 Agents to 2016 and running two environments

The following upgrade path supports customers in an Operations Manager scenario with parallel environments, sharing agents, so that the original System Center 2012 R2 Operations Manager environment is left intact. After the upgrade, the agents have been upgraded to System Center 2016 Operations Manager and are fully capable of working with native System Center 2012 R2 Operations Manager functionality.  

1. Retain the original System Center 2012 R2 Operations Manager environment.

2. Set up an additional, new System Center 2016 - Operations Manager environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, console, web console, and reporting server.

3. Upgrade the System Center 2012 R2 Operations Manager Agents to 2016.

   a. Push-Install option

   b. Manual / Command-line option

## Next steps

- To understand the pre-upgrade tasks you should perform to complete the upgrade to your management group, see [Pre-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](pre-upgrade-tasks-when-upgrading-to-system-center-2016-operations-manager.md).

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](post-upgrade-tasks-when-upgrading-to-system-center-2016-operations-manager.md).