---
title: How to Upgrade OM2012 SP1 Agents to OM2012 R2  Parallel Environments
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c5997cc-3b31-4c0d-855e-d2b8ab75a018
author:mgoedtel
manager:cfreemanwa
---
# How to Upgrade OM2012 SP1 Agents to OM2012 R2  Parallel Environments
This upgrade path contains an [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] scenario with parallel environments, sharing agents, so that the original [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] environment is left intact.  After the upgrade, the agents have been upgraded to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] and are fully capable of working with native [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] functionality.  The [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] agents are also able to “talk” to the [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] management server.  
  
## Upgrading OM2012 SP1 Agents to OM2012 R2 using Parallel Environments  
If you want to maintain your [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] environment you can install [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] in parallel and just upgrade your agents using the following process.  
  
1.  Retain the original [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] environment.  
  
2.  Set up an additional, new [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] environment with management servers, gateway, Operations Manager Database, Operations Manager Data Warehouse, console, web console, and reporting server. See [Deploying System Center 2012 \- Operations Manager](assetId:///969a31d6-5ef2-4127-9cfe-0af66c981b6c) for more information.  
  
3.  Upgrade the [!INCLUDE[sc2012sp1_long](../../om/manage/includes/sc2012sp1_long_md.md)], [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] Agents to 2012 R2 using Push\-Install or Command Line options as appropriate. See [How to Upgrade an Agent to System Center 2012 R2  Operations Manager](../Topic/How%20to%20Upgrade%20an%20Agent%20to%20System%20Center%202012%20R2%20%20Operations%20Manager.md) for more information.  
  
