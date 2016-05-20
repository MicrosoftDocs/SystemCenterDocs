---
title: Adding Windows servers as Hyper-V hosts or host clusters in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b6a008d-0139-47af-8804-ed0ff75e5e88
---
# Adding Windows servers as Hyper-V hosts or host clusters in VMM
The procedures in this section describe how to add an existing Windows Server computer or a Windows Server failover cluster as one or more managed Hyper\-V hosts in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]. For information about other ways to add servers or clusters, see [Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md) and [Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

|Procedure|Description|
|-------------|---------------|
|[Prerequisites: adding servers or clusters as Hyper-V hosts or host clusters in VMM](Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)|Lists important prerequisites that apply to servers or clusters in any of the following locations \(in relation to the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server\):<br /><br />-   In the same Active Directory domain or a domain with a two\-way trust<br />-   In an untrusted domain<br />-   In a disjointed namespace|
|[How to add existing servers or clusters as Hyper-V hosts or host clusters in VMM](How-to-add-existing-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)|Describes how to add existing servers or clusters as Hyper\-V hosts or host clusters. The servers or clusters can be in any of the locations listed in the previous row of this table.|
|[How to add Hyper-V hosts in a perimeter network in VMM](How-to-add-Hyper-V-hosts-in-a-perimeter-network-in-VMM.md)|Describes how to add Hyper\-V hosts that are in a perimeter network, also known as DMZ, demilitarized zone, and screened subnet. \([!INCLUDE[vmm12short](Token/vmm12short_md.md)] does not support managing a host cluster in a perimeter network.\)<br /><br />To manage a stand\-alone host in a workgroup rather than a domain, treat it as a host in a perimeter network.|

## Example naming overview
The example names in this section are intended to demonstrate the concepts used when adding Windows servers as Hyper\-V hosts or host clusters in [!INCLUDE[vmm12short](Token/vmm12short_md.md)].

The following table summarizes the example names that could be used in this scenario. Some of these names are also used in examples in procedures in this section.

> [!NOTE]
> The example resource names and configuration are used to help demonstrate the concepts. You can adapt them to your test environment.

|Resource|Example of resource name|
|------------|----------------------------|
|Windows Server in a trusted Active Directory domain|**HyperVHost01.contoso.com**|
|Windows Server in an untrusted Active Directory domain|**HyperVHost02.fabrikam.com**|
|Windows Server in a disjointed namespace|**HyperVHost03.contosocorp.com**|
|Windows Server in a perimeter network|**HyperVHost04**|
|Host groups|-   **HyperVHost01.contoso.com** could be added to the host group **Seattle\\SEA\_Tier0**<br />-   **HyperVHost02.fabrikam.com** could be added to the host group **New York\\NY\_Tier2**<br />-   **HyperVHost03** could be added to the host group **New York\\NY\_Tier1**<br />-   **HyperVHost04** could be added to the host group **Seattle\\SEA\_Tier2**|
|Run As accounts|-   **Trusted Hyper\-V Hosts** **Note:**     This Run As account is optional, as you can also specify a user name and password.<br />-   **Untrusted Hyper\-V Hosts**|

## See Also
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)


