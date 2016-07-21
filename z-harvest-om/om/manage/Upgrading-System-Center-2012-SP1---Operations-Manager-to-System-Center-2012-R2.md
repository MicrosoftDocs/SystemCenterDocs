---
title: Upgrading System Center 2012 SP1 - Operations Manager to System Center 2012 R2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75cd57fb-7369-40e8-abe0-9d9915a56ba0
author:mgoedtel
manager:cfreemanwa
---
# Upgrading System Center 2012 SP1 - Operations Manager to System Center 2012 R2
This Upgrade Guide provides information about how to upgrade from [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)].  
  
> [!WARNING]  
> If you are upgrading two or more System Center components, you must follow the procedures that are documented in [Upgrade Sequencing for System Center 2012 R2](http://go.microsoft.com/fwlink/?LinkId=328675).  
>   
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:  
>   
> 1.  [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)]  
> 2.  [!INCLUDE[smshort12](../../om/manage/includes/smshort12_md.md)]  
> 3.  [!INCLUDE[dpm2012sp1long](../../om/manage/includes/dpm2012sp1long_md.md)]  
> 4.  [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)]  
> 5.  [!INCLUDE[cmshort](../../om/manage/includes/cmshort_md.md)]  
> 6.  [!INCLUDE[vmm12sp1_med](../../om/manage/includes/vmm12sp1_med_md.md)]  
> 7.  [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)]  
  
> [!WARNING]  
> The only supported upgrade path to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] is from [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)]. If you are upgrading from [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], you must first upgrade to [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] before upgrading to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)]. See [Upgrading to System Center 2012 \- Operations Manager](assetId:///2c9094d2-a57f-4d77-b430-f7ee2cbede6f) and [Upgrading System Center 2012 - Operations Manager to System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=309041) for complete upgrade information.  
  
> [!IMPORTANT]  
> It is assumed in this guide that you are performing an *upgrade* to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)]. For information about installing [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] on a computer where no previous version of [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] exists, see [Deploying System Center 2012 \- Operations Manager](http://go.microsoft.com/fwlink/?LinkId=309317).  
  
Before you upgrade to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)], you must first determine whether all servers in your [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] management group meet the minimum supported configurations. For more information, see [System Requirements: System Center 2012 R2 Operations Manager](http://go.microsoft.com/fwlink/?LinkId=309038)  
  
There are several options for upgrade:  
  
1.  If you run upgrade on a single\-server management group, you only need to run upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation will not continue until you resolve all issues.  
  
2.  If you are upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting and Audit Collection Services \(ACS\). You must also perform a number of pre\-upgrade and post\-upgrade tasks.  
  
3.  If you want to maintain your Operations Manager 2007 R2 environment you can install System Center 2012 Service Pack 1 \(SP1\), Operations Manager in parallel and just upgrade your agents.  
  
## High Level View of System Center 2012 R2 Operations Manager Upgrade Steps - Upgrading a Distributed Management Group  
The following steps outline the process for upgrading a distributed management group:  
  
1.  Accomplish Pre\-Upgrade Tasks  
  
2.  Upgrade the initial management server and then additional management servers \(each management server must be upgraded\)  
  
3.  Upgrade ACS \(because the ACS server must be on same machine as a management server, we recommend you perform this step along with the upgrade of the management server on which ACS resides.\)  
  
4.  \*Upgrade Gateway\(s\)  
  
5.  Upgrade Console  
  
6.  Push Install to Agent\(s\) \/ Upgrading Manually Installed Agents  
  
7.  Upgrade Web Console  
  
8.  Upgrade Reporting Server  
  
9. Accomplish Post\-Upgrade Tasks  
  
\* Steps 4 to 8 after Management Server Upgrade can occur in parallel.  
  
## High Level View of System Center 2012 R2 Operations Manager Upgrade Steps - Upgrading 2012 SP1 Agents to 2012 R2 and Running Two Environments  
The following upgrade path supports customers in an [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] scenario with parallel environments, sharing agents, so that the original [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] environment is left intact.  After the upgrade, the agents have been upgraded to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] and are fully capable of working with native [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] functionality.  The R2 agents are also able to "talk" to the [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] management server.  
  
> [!IMPORTANT]  
> In this parallel environment scenario, we support upgrade of [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agents with the latest cumulative update \(Operations Manager 2007 R2 CU6\).  
  
1.  Retain the original [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] environment.  
  
2.  Set up an additional, new [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, console, web console, and reporting server.  
  
3.  Upgrade the [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] Agents to 2012 R2.  
  
    a. Push\-Install option  
  
    b. Manual \/ Command Line option  
  
    > [!NOTE]  
    > If you are manually upgrading, step 2 is not needed.  
  
