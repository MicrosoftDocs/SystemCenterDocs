---
title: How to configure host group properties in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb546ae6-3fed-4bef-991b-fff1d76614ef
---
# How to configure host group properties in VMM
You can use the following procedure to configure host group properties in Virtual Machine Manager \(VMM\).

### To configure host group properties

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, expand **All Hosts**, and then click the host group that you want to configure.

3.  On the **Folder** tab, in the **Properties** group, click **Properties**.

4.  Configure any of the following settings:

    |Tab|Settings|
    |-------|------------|
    |**General**|Configure the host group name, the location in the host group hierarchy, the description, and whether to allow unencrypted BITS file transfers.|
    |**Placement Rules**|VMM automatically identifies the most suitable host to which you can deploy virtual machines. However, you can specify custom placement rules. By default, a host group uses the placement settings from the parent host group.|
    |**Host Reserves**|Host reserve settings specify the amount of resources that VMM sets aside for the host operating system to use. For a virtual machine to be placed on a host, the host must be able to meet the virtual machine’s resource requirements without using host reserves. You can set host reserves for individual host groups and for individual hosts. The host reserve settings for the root host group, All Hosts, sets the default host reserves for all hosts.<br /><br />You can configure reserve values for the following resources:<br /><br />-   CPU<br />-   Memory<br />-   Disk I\/O<br />-   Disk space<br />-   Network I\/O|
    |**Dynamic Optimization**|Configure dynamic optimization and power optimization settings. Dynamic optimization balances the virtual machines load within a host cluster. Power optimization enables VMM to evacuate hosts of a balanced cluster and turn them off to save power. For more information about these settings, see [Configuring dynamic optimization and power optimization in VMM](Configuring-dynamic-optimization-and-power-optimization-in-VMM.md).|
    |**Network**|View inheritance settings, and configure whether to inherit network logical resources from parent host groups. The network logical resources include the following:<br /><br />-   IP address pools<br />-   Load balancers<br />-   Logical networks<br />-   MAC address pools|
    |**Storage**|View and allocate storage to a host group. For more information, see the following topics:<br /><br />-   [How to allocate storage logical units to a host group in VMM](How-to-allocate-storage-logical-units-to-a-host-group-in-VMM.md)<br />-   [How to allocate storage pools to a host group in VMM](How-to-allocate-storage-pools-to-a-host-group-in-VMM.md)|
    |**Custom Properties**|Manage custom properties for the following object types:<br /><br />-   Virtual machine<br />-   Virtual machine template<br />-   Host<br />-   Host cluster<br />-   Host group<br />-   Service template<br />-   Service instance<br />-   Computer tier<br />-   Cloud|

## See Also
[Overview: using host groups in VMM](Overview--using-host-groups-in-VMM.md)
[How to create a host group structure in VMM](How-to-create-a-host-group-structure-in-VMM.md)
[Managing host groups in VMM](Managing-host-groups-in-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


