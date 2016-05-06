---
title: How to Configure Agent Failover to Multiple Gateway Servers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f6532e7-6bbd-441e-8a3c-9dec577c8724
---
# How to Configure Agent Failover to Multiple Gateway Servers
If you have deployed multiple gateway servers in a domain that does not have a trust relationship established with the domain that the rest of the management group is in, you can configure agents to utilize those gateway servers as necessary. To do this, you must use the Operations Manager Shell to configure an agent to fail over to multiple gateway servers. The commands can be run from any command shell in the management group.

> [!IMPORTANT]
> When changing the primary management server of an agent, allow the agent to connect to its new primary management server before making changes to its failover server. Allowing the agent to get current topology information from the new primary management server prevents the agent from losing communication with all management servers.

### To configure agent failover to multiple gateway servers

1.  Log on to the computer with an account that is a member of the Administrators group.

2.  Click **Start**, click **All Programs**, click **Microsoft System Center 2012**, click **Operations Manager**, and then click **Operations Manager Shell**.

3.  In Operations Manager Shell, run the following command:

    ```
    $primaryMS = Get-SCOMManagementServer –Name “<name of primary server>”
    $failoverMS = Get-SCOMManagementServer –Name “<name of 1st failover>”,”<name of 2nd failover>”,…,”<name of nth failover>”
    $agent = Get-SCOMAgent –Name “<name of agent>”

    Set-SCOMParentManagementServer –Agent $agent –PrimaryServer $primaryMS
    Set-SCOMParentManagementServer –Agent $agent –FailoverServer $failoverMS

    ```

    For help with the Set\-SCOMParentManagementServer command, type the following in the command shell window:

    ```
    Get-help Set-SCOMParentManagementServer -full
    ```

## See Also
[Monitoring Across Untrusted Boundaries in Operations Manager](../Topic/Monitoring-Across-Untrusted-Boundaries-in-Operations-Manager.md)
[About Gateway Servers in Operations Manager](../Topic/About-Gateway-Servers-in-Operations-Manager.md)
[Determining the Health of Gateway Servers](../Topic/Determining-the-Health-of-Gateway-Servers.md)
[Using Multiple Gateway Servers](../Topic/Using-Multiple-Gateway-Servers.md)
[How to Configure a Gateway Server to Failover Between Multiple Management Servers](../Topic/How-to-Configure-a-Gateway-Server-to-Failover-Between-Multiple-Management-Servers.md)
[Certificate Renewal for Gateway Servers and Management Servers](../Topic/Certificate-Renewal-for-Gateway-Servers-and-Management-Servers.md)

