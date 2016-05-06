---
title: How to Configure a Gateway Server to Failover Between Multiple Management Servers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7587e60-8f21-4ee8-ade1-702df98ddebb
---
# How to Configure a Gateway Server to Failover Between Multiple Management Servers
Use the Get\-ManagementServer\-GatewayManagementServer cmdlet in the Operations Manager Shell as shown in the following example to configure a gateway server to fail over to multiple management servers. The commands can be run from any command shell in the management group.

### To configure gateway server failover to multiple management servers

1.  Log on to the gateway server with an account that is a member of the Administrators role for the management group.

2.  Click **Start**, click **All Programs**, click **Microsoft System Center 2012**, click **Operations Manager**, and then click **Operations Manager Shell**.

3.  In Operations Manager Shell, run the following command:

    ```
    $primaryMS = Get-SCOMManagementServer –Name “<name of primary server>”
    $failoverMS = Get-SCOMManagementServer –Name “<name of 1st failover>”,”<name of 2nd failover>”,…,”<name of nth failover>”
    $gatewayMS = Get-SCOMGatewayManagementServer –Name “<name of gateway>”

    Set-SCOMParentManagementServer –Gateway $gatewayMS –PrimaryServer $primaryMS
    Set-SCOMParentManagementServer –Gateway $gatewayMS –FailoverServer $failoverMS

    ```

    For help with the Set\-SCOMParentManagementServer command, type the following in the command shell window.

    ```
    Get-help Set-SCOMParentManagementServer -full
    ```

## See Also
[Monitoring Across Untrusted Boundaries in Operations Manager](../Topic/Monitoring-Across-Untrusted-Boundaries-in-Operations-Manager.md)
[About Gateway Servers in Operations Manager](../Topic/About-Gateway-Servers-in-Operations-Manager.md)
[Using Multiple Gateway Servers](../Topic/Using-Multiple-Gateway-Servers.md)
[Determining the Health of Gateway Servers](../Topic/Determining-the-Health-of-Gateway-Servers.md)
[How to Configure Agent Failover to Multiple Gateway Servers](../Topic/How-to-Configure-Agent-Failover-to-Multiple-Gateway-Servers.md)
[Certificate Renewal for Gateway Servers and Management Servers](../Topic/Certificate-Renewal-for-Gateway-Servers-and-Management-Servers.md)

