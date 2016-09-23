---
title:  How to Upgrade Agents in a Parallel Deployment
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Upgrade Agents in a Parallel Deployment

>Applies To: System Center 2016 - Operations Manager

When you perform a side-by-side deployment of System Center 2016 - Operations Manager (also referred to as a parallel deployment) with your existing System Center 2012 R2 Operations Manager management group, you can continue to proactively monitor your workloads and maintain insight into the availability of your critical services.  The agents reporting to the Operations Manager 2012 R2 management group can be upgraded to System Center 2016 - Operations Manager and are fully capable of communicating with both management groups until you migrate and retire the Operations Manager 2012 R2 management group.  

## Upgrading agents to System Center 2016 - Operations Manager

If you want to maintain your System Center 2012 R2 Operations Manager environment you can install System Center 2016 - Operations Manager in parallel and just upgrade your agents depending on what method you use today.  Such as:

- The discovery and installation of one or more agents from the Operations console.  
    If you discover and install the existing agent-managed system from the new Operations Manager 2016 management group, the agent will be upgraded and multi-homed to where it reports to both management groups.  
- Inclusion in the installation image.  
    Your image will need to be updated to include the new version and configured to assign the agent to the new Operations Manager 2016 management group.   
- Manual installation where setup is manually executed on the agent or deployed through an existing software distribution tool.  
    Your deployment process will need to be updated to inlucde the new agent Windows installer package and dependencies required.  The logic defined to interrogate, install and configure, and verify the agent will need to be revised accordingly.   


Once you have completed all the post-upgrade steps and are comfortable with the state of your new Operations Manager 2016 management group, you can reconfigure the agents to remove assignment from the Operations Manager 2012 R2 management group.  This can be accomplished by uninstalling the agent from the Operations console in the Operations Manager 2012 R2 management group, which won't uninstall the agent but will only remove the configuration.  You can also follow the guidance in the Operations Manager SDK to programatically [remove the management group configuration](https://msdn.microsoft.com/library/hh329017.aspx) from the agent.  



