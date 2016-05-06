---
title: Preparing the fabric scenario in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90b57d6b-bbeb-4949-867c-0a4fdd1faf8a
---
# Preparing the fabric scenario in VMM
The example scenario that is used in this section illustrates one way to configure the fabric with [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], including sample host groups, library shares, networking resources, and storage resources. Because some of these examples depend on your existing hardware and physical infrastructure, consider the examples as guidelines. For more information, see the topics listed in [Managing Fabric Resources in VMM](Managing-fabric-resources-in-VMM.md).

The following table summarizes a set of sample **RESOURCES** that you could create to try out a sample infrastructure.

> [!NOTE]
> The example resource names and configuration are used to help demonstrate the concepts. You can adapt them to your test environment.

-   Host Groups

    |||
    |-|-|
    |Seattle|Tier0\_SEA|
    ||Tier1\_SEA|
    ||Tier2\_SEA|
    |New York|Tier0\_NY|
    ||Tier1\_NY|
    ||Tier2\_NY|

-   Library Shares

    ||
    |-|
    |VMMServer01\\SEALIbrary \(in Seattle\)|
    |NYLibrary01\\NYLIbrary<br /><br />\(in New York\)|

-   Networking

    Logical Networks:

    |Name|Description|
    |--------|---------------|
    |**PUBLIC**|**Public network. Use for Internet\-facing Web servers.**|
    |**Management**|**Network for host management.** **Note:** In the examples, only the **Management** logical network is fully defined with example network sites, example IP subnets assigned and an example static IP address pool.|
    |**LAB**|**Lab network. Use for test and development labs.**|

    Network sites for the **Management** logical network:

    |Name|Subnet|Management|
    |--------|----------|--------------|
    |**Management \- Seattle**|**10.0.0.0\/24**|**7**|
    |**Management – New York**|**172.16.0.0\/24**|**12**|

    IP address pool:

    |||
    |-|-|
    |Name|**Management \- Seattle IP pool**|
    |Description|**IP addresses for host management \- Seattle**|
    |Begin IP address|**10.0.0.10**|
    |End IP address|**10.0.0.99**|
    |Reserved range for virtual IP addresses associated with load balancers:|**10.0.0.25 – 10.0.0.35**|
    |Default gateway|**10.0.0.1**|
    |DNS server|**10.0.0.2**|
    |WINS server|**10.0.0.3**|

    MAC address pool:

    |||
    |-|-|
    |Name|**MAC pool \- Seattle**|
    |Starting address|**00:1D:D8:B7:1C:00**|
    |Ending address|**00:1D:D8:B7:1F:E8**|

    Load Balancer:

    |||
    |-|-|
    |Name|**LoadBalancer01.contoso.com**|
    |VIP template|**Web tier \(HTTPS traffic\)**|

-   Storage

    Storage classifications:

    |Name|Description|
    |--------|---------------|
    |**GOLD**|**Storage pool based on solid\-state drives \(SSDs\) that delivers high performance for I\/O intensive applications**|
    |**SILVER**|**Fibre Channel Serial Attached SCSI \(SAS\) storage \(RAID 5\)**|
    |**BRONZE**|**iSCSI Serial ATA \(SATA\) storage \(RAID 5\)**|

## See Also
[Managing host groups in VMM](../Topic/Managing-host-groups-in-VMM.md)
[Configuring the VMM library](../Topic/Configuring-the-VMM-library.md)
[Managing network resources with VMM](../Topic/Managing-network-resources-with-VMM.md)
[Managing hosts and host clusters with VMM](../Topic/Managing-hosts-and-host-clusters-with-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources in VMM](../Topic/Managing-fabric-resources-in-VMM.md)

