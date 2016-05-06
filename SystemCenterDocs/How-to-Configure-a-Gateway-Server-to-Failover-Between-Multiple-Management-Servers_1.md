---
title: How to Configure a Gateway Server to Failover Between Multiple Management Servers_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38142d97-8614-44ec-97d0-2c26c99405b8
---
# How to Configure a Gateway Server to Failover Between Multiple Management Servers_1
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
[Monitoring Across Untrusted Boundaries in Operations Manager](./Monitoring-Across-Untrusted-Boundaries-in-Operations-Manager.md)
[About Gateway Servers in Operations Manager](./About-Gateway-Servers-in-Operations-Manager.md)
[Using Multiple Gateway Servers](./Using-Multiple-Gateway-Servers.md)
[Determining the Health of Gateway Servers](./Determining-the-Health-of-Gateway-Servers.md)
[How to Configure Agent Failover to Multiple Gateway Servers](./How-to-Configure-Agent-Failover-to-Multiple-Gateway-Servers.md)
[Certificate Renewal for Gateway Servers and Management Servers](./Certificate-Renewal-for-Gateway-Servers-and-Management-Servers.md)


