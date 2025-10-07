---
title: Configure Agent Failover to Multiple Gateway Servers
description: This article describes how to use PowerShell to configure failover between multiple Gateway servers.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: 4f6532e7-6bbd-441e-8a3c-9dec577c8724
---
# Configure Agent Failover to Multiple Gateway Servers



If you've deployed multiple gateway servers in a domain that doesn't have a trust relationship established with the domain that the rest of the management group is in, you can configure agents to utilize those gateway servers as necessary. To do this, you must use the Operations Manager Shell to configure an agent to fail over to multiple gateway servers. The commands can be run from any command shell in the management group.  

> [!IMPORTANT]  
> When changing the primary management server of an agent, allow the agent to connect to its new primary management server before making changes to its failover server. Allowing the agent to get current topology information from the new primary management server prevents the agent from losing communication with all management servers.  

## Configure agent failover to multiple gateway servers

Follow these steps to configure agent failover to multiple gateway servers:

1. Sign in to the computer with an account that is a member of the Administrators group.  

2. Select **Start**, select **All Programs**, select **Microsoft System Center&nbsp;2012**, select **Operations Manager**, and then select **Operations Manager Shell**.  

3. In Operations Manager Shell, run the following command:  

    ```  
    $primaryMS = Get-SCOMManagementServer -Name "<name of primary server>"  
    $failoverMS = Get-SCOMManagementServer -Name "<name of 1st failover>","<name of 2nd failover>",...,"<name of nth failover>"  
    $agent = Get-SCOMAgent -Name "<name of agent>"  

    Set-SCOMParentManagementServer -Agent $agent -PrimaryServer $primaryMS  
    Set-SCOMParentManagementServer -Agent $agent -FailoverServer $failoverMS  

    ```  

    For help with the Set\-SCOMParentManagementServer command, enter the following in the command shell window:  

    ```  
    Get-help Set-SCOMParentManagementServer -full  
    ```  

## Next steps

To understand how to manage the configuration settings of a Windows agent and the options available, review [Configuring Windows Agents](manage-deploy-config-windows-agent.md).
