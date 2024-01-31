---
ms.assetid: 71cf60f4-e6fb-4250-a9d3-64eff209e0cc
title: How to Upgrade Agents in a Parallel Deployment
description: This article provides guidance with upgrading agents when planning a side-by-side migration to Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 08/22/2023
ms.custom: UpdateFrequency.5, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# How to upgrade agents in a parallel deployment

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

When you perform a side-by-side deployment of System Center 2016 - Operations Manager or System Center Operations Manager 1801 from a previous version (also referred to as a parallel deployment) with your existing Operations Manager management group, you can continue to proactively monitor your workloads and maintain insight into the availability of your critical services.  

::: moniker range="sc-om-1801"

The following coexistence scenarios are supported for the Operations Manager agent in a parallel deployment scenario with System Center Operations Manager 1801.

* System Center 2016 - Operations Manager RTM and higher
* System Center Operations Manager 2012 R2 RTM and higher

Agents reporting to your Operations Manager 2012 R2 or 2016 management group can be upgraded to System Center Operations Manager 1801 and are fully capable of communicating with both management groups until you complete your migration and retire the old management group.  

::: moniker-end

Agents reporting to your Operations Manager 2012 R2 management group can be upgraded to System Center 2016 - Operations Manager and are fully capable of communicating with both management groups until you complete your migration and retire the Operations Manager 2012 R2 management group.  

## Upgrading agents

If you want to maintain your existing Operations Manager environment, you can install the latest release of Operations Manager in parallel, and just upgrade your agents depending on what method you currently use.  Such as:

- The discovery and installation of one or more agents from the Operations console.

    If you discover and install the existing agent-managed system from the new Operations Manager management group, the agent will be upgraded and multi-homed to where it reports to both management groups.  

- Inclusion in the installation image.  

    Your image will need to be updated to include the new version and configured to assign the agent to the new Operations Manager management group.

- Manual installation where setup is manually executed on the agent or deployed through an existing software distribution tool.  

    Your deployment process will need to be updated to include the new agent Windows installer package and dependencies required. The logic defined to interrogate, install and configure, and verify the agent will need to be updated accordingly.

Once you've completed all the post-upgrade steps and are comfortable with the state of your new Operations Manager management group, you can reconfigure the agents to remove assignment from the existing Operations Manager management group that you're preparing to retire.  This can be accomplished by following the guidance in the Operations Manager SDK to programatically [remove the management group configuration](/previous-versions/system-center/developer/hh329017(v=msdn.10)) from the agent.  

## Next steps

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).  

- To understand the options and steps for installing agents and discovering objects to be monitored by Operations Manager, review information in the [Managing Discovery and Agents](welcome.md) section.

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).
