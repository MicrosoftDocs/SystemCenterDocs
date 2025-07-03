---
ms.assetid: 71cf60f4-e6fb-4250-a9d3-64eff209e0cc
title: Upgrade Agents in a Parallel Deployment
description: This article provides guidance with upgrading agents when planning a side-by-side migration to Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 03/03/2025
ms.custom: UpdateFrequency.5, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade agents in a parallel deployment

::: moniker range="sc-om-2016"

When you perform a side-by-side deployment of System Center 2016 - Operations Manager or System Center Operations Manager 2019 from a previous version (also referred to as a parallel deployment) with your existing Operations Manager management group, you can continue to proactively monitor your workloads and maintain insight into the availability of your critical services.

::: moniker-end

::: moniker range="sc-om-2019"

When you perform a side-by-side deployment of System Center 2019 - Operations Manager or System Center Operations Manager 2016 from a previous version (also referred to as a parallel deployment) with your existing Operations Manager management group, you can continue to proactively monitor your workloads and maintain insight into the availability of your critical services.

::: moniker-end

::: moniker range="sc-om-2022"

When you perform a side-by-side deployment of System Center 2022 - Operations Manager or System Center Operations Manager 2019 from a previous version (also referred to as a parallel deployment) with your existing Operations Manager management group, you can continue to proactively monitor your workloads and maintain insight into the availability of your critical services.

::: moniker-end

::: moniker range="sc-om-2025"

When you perform a side-by-side deployment of System Center 2025 - Operations Manager or System Center Operations Manager 2022 from a previous version (also referred to as a parallel deployment) with your existing Operations Manager management group, you can continue to proactively monitor your workloads and maintain insight into the availability of your critical services.

::: moniker-end

::: moniker range="sc-om-2016"

Agents reporting to your Operations Manager 2012 R2 management group can be upgraded to System Center 2016 - Operations Manager and are fully capable of communicating with both management groups until you complete your migration and retire the Operations Manager 2012 R2 management group. 

::: moniker-end

::: moniker range="sc-om-2019"

Agents reporting to your Operations Manager 2016 management group can be upgraded to System Center 2019 - Operations Manager and are fully capable of communicating with both management groups until you complete your migration and retire the Operations Manager 2016 management group.

::: moniker-end

::: moniker range="sc-om-2022"

Agents reporting to your Operations Manager 2019 management group can be upgraded to System Center 2022 - Operations Manager and are fully capable of communicating with both management groups until you complete your migration and retire the Operations Manager 2019 management group.

::: moniker-end

::: moniker range="sc-om-2025"

Agents reporting to your Operations Manager 2022 management group can be upgraded to System Center 2025 - Operations Manager and are fully capable of communicating with both management groups until you complete your migration and retire the Operations Manager 2022 management group.

::: moniker-end

## Upgrade agents

If you want to maintain your existing Operations Manager environment, you can install the latest release of Operations Manager in parallel, and just upgrade your agents depending on what method you currently use. Such as:

- The discovery and installation of one or more agents from the Operations console

    If you discover and install the existing agent-managed system from the new Operations Manager management group, the agent will be upgraded and multi-homed to where it reports to both management groups.  

- Inclusion in the installation image

    Your image will need to be updated to include the new version and configured to assign the agent to the new Operations Manager management group.

- Manual installation where setup is manually executed on the agent or deployed through an existing software distribution tool

    Your deployment process will need to be updated to include the new agent Windows installer package and dependencies required. The logic defined to interrogate, install and configure, and verify the agent will need to be updated accordingly.

Once you've completed all the post-upgrade steps and are comfortable with the state of your new Operations Manager management group, you can reconfigure the agents to remove assignment from the existing Operations Manager management group that you're preparing to retire. This can be accomplished by following the guidance in the Operations Manager SDK to programatically [remove the management group configuration](/previous-versions/system-center/developer/hh329017(v=msdn.10)) from the agent.  

## Next steps

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).  
- To understand the options and steps for installing agents and discovering objects to be monitored by Operations Manager, review information in the [Manage Discovery and Agents](welcome.md) section.
- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).
