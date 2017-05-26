---
title: How to Configure Agent Failover to Multiple Gateway Servers
description: This article describes how to use PowerShell to configure failover between multiple Gateway servers.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 05/24/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 4f6532e7-6bbd-441e-8a3c-9dec577c8724
---
# How to Configure Agent Failover to Multiple Gateway Servers

If you have deployed multiple gateway servers in a domain that does not have a trust relationship established with the domain that the rest of the management group is in, you can configure agents to utilize those gateway servers as necessary. To do this, you must use the Operations Manager Shell to configure an agent to fail over to multiple gateway servers. The commands can be run from any command shell in the management group.  
  
> [!IMPORTANT]  
> When changing the primary management server of an agent, allow the agent to connect to its new primary management server before making changes to its failover server. Allowing the agent to get current topology information from the new primary management server prevents the agent from losing communication with all management servers.  
  
## To configure agent failover to multiple gateway servers  
  
1.  Log on to the computer with an account that is a member of the Administrators group.  
  
2.  Click **Start**, click **All Programs**, click **Microsoft System Center&nbsp;2012**, click **Operations Manager**, and then click **Operations Manager Shell**.  
  
3.  In Operations Manager Shell, run the following command:  
  
    ```  
    $primaryMS = Get-SCOMManagementServer -Name "<name of primary server>"  
    $failoverMS = Get-SCOMManagementServer -Name "<name of 1st failover>","<name of 2nd failover>",...,"<name of nth failover>"  
    $agent = Get-SCOMAgent -Name "<name of agent>"  
  
    Set-SCOMParentManagementServer -Agent $agent -PrimaryServer $primaryMS  
    Set-SCOMParentManagementServer -Agent $agent -FailoverServer $failoverMS  
  
    ```  
  
    For help with the Set\-SCOMParentManagementServer command, type the following in the command shell window:  
  
    ```  
    Get-help Set-SCOMParentManagementServer -full  
    ```  
  
## Next steps 
To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Windows Agents](manage-deploy-config-windows-agent.md).
  
