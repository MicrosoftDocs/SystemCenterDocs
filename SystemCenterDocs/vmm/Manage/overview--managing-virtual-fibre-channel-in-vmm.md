---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Overview  managing Virtual Fibre Channel in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  81189655-4e01-4a55-8d7d-be8dd62e3d8b
---

# Overview: managing Virtual Fibre Channel in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

This topic provides background information to help you understand Virtual Fibre Channel in Virtual Machine Manager (VMM).

Virtual Fibre Channel enables Hyper-V virtual machines (VMs) on host computers to have direct access to Fibre Channel storage area network (SAN) array resources. In this way, you can virtualize applications and workloads that require direct access to SAN logical unit numbers (LUNs). Using Virtual Fibre Channel, VM failover clusters can also access Fibre Channel SAN arrays.

For a list of procedures for configuring Virtual Fibre Channel in VMM, see [Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md).

In this topic:

-   [Glossary of terms](Overview--managing-Virtual-Fibre-Channel-in-VMM.md#BKMK_glossary)

-   [Supported configurations](Overview--managing-Virtual-Fibre-Channel-in-VMM.md#BKMK_supported)

-   [Prerequisites](Overview--managing-Virtual-Fibre-Channel-in-VMM.md#BKMK_prerequisites)

-   [Steps to deploy Virtual Fibre Channel](Overview--managing-Virtual-Fibre-Channel-in-VMM.md#BKMK_deploy)

## <a name="BKMK_glossary"></a>Glossary of terms
The following terms represent the most important elements of a Virtual Fibre Channel environment:

**Fabric**.  A fabric is one or more Fibre Channel switches that are connected together using Fibre Channel cables. Fabrics are used to access Fibre Channel storage devices. Although the term fabric is generally used to indicate multiple switches, a fabric can be comprised of a single switch.

**Switch**. A Fibre Channel switch is a network switch comprised of multiple ports and that supports the Fibre Channel (FC) transport protocol.

**Classification**. A friendly name used to designate a fabric for use in templates. Fabrics can be classified according to availability or service level, for example.

**HBA**. Host Bus Adapters (HBAs) are network cards installed in host computers and are used to provide connectivity to Fibre Channel devices. Every HBA card is assigned a World Wide Node Name (WWNN), which is shared among each port on the HBA. In turn, each HBA port is assigned a World Wide Port Name (WWPN). HBA ports are referred to as initiator ports.

**NPIV**. N_Port ID Virtualization (NPIV) is a standard used to create and map multiple virtual Fibre Channel (vHBA) ports to a single physical Fibre Channel N_port.

**vHBA**. The virtualized HBA. Multiple vHBAs can be mapped to a single HBA. The vHBA uses NPIV to address a VM"s WWN within a host HBA.

**Virtual SAN**. In the context of VMM, a virtual SAN (vSAN) defines a group of physical Fibre Channel ports that are connected to a physical SAN array. Not to be confused with the vSAN product by VMware.

**WWNN**. World Wide Node Name (WWNN) is a globally unique number assigned to a Fibre Channel switch, HBA card, storage drive or other endpoint device.

**WWPN**. World Wide Port Number (WWPN) is a globally unique number assigned to a Fibre Channel port, similar to that of an Ethernet MAC address. The WWPN allows the storage fabric to recognize a particular HBA port.

**Zone**. A collection of Fibre Channel ports that are permitted to communicate with each other on a storage fabric

**Zoning**. A method of subdividing a storage area network into separate zones, or subsets of nodes on the network.

**Zone alias**. Several zone members that are grouped together and designated with a friendly name.

**Zone members**. Any device with a WWNN that is attached to a storage fabric and belongs to a zone.

**Zone set**. A database of zone definitions that fabrics use to determine traffic routes. All Fibre Channel switches keep a copy of the zone set. An active zone set refers to all the zones that are available to the fabric. An inactive zone set refers to those zones whose information has not yet been propagated to the fabric and hence are not available to the fabric. Zone information is always changed or updated in an inactive zone set first; such information cannot be changed in an active zone set.

## <a name="BKMK_supported"></a>Supported configurations
VMM supports the following Virtual Fibre Channel configurations:

-   Single storage array connected to a single fabric (comprised of single or multiple switches) connected to a single vSAN.

-   Single storage array connected to multiple fabrics (comprised of single or multiple switches per fabric) connected to a single vSAN.

-   Multiple storage arrays connected to a single fabric (comprised of single or multiple switches) connected to a single vSAN.

-   Multiple storage arrays connected to multiple fabrics (comprised of single or multiple switches per fabric) connected to multiple vSANs. This configuration provides dual-redundant paths to storage arrays.

> [!NOTE]
> A vSAN can only include HBAs from a single fabric.

## <a name="BKMK_prerequisites"></a>Prerequisites
In order to successfully deploy Virtual Fibre Channel in your network environment, the following prerequisites must be met:

-   Ensure that the latest firmware and drivers are installed for storage arrays, switches and HBAs.

-   Ensure that storage arrays can present logical units (LUs).

-   Enable NPIV on Fibre Channel switches and HBAs.

-   Host computers must be running at least Windows Server 2012.

-   Ensure that an SMI-S provider is installed. VMM manages Fibre Channel fabrics and SAN devices using the SMI-S provider.

## <a name="BKMK_deploy"></a>Configuring Virtual Fibre Channel with VMM
Complete the following steps to integrate Virtual Fibre Channel with your VMM environment:

|Step|More information|
|--------|--------------------|
|Discover Fibre Channel fabrics and assign classifications to each fabric.|[How to discover and classify Virtual Fibre Channel Fabrics with VMM](How-to-discover-and-classify-Virtual-Fibre-Channel-Fabrics-with-VMM.md)|
|For each host computer that VMM manages, create vSANs by grouping host HBA ports.|[How to manage vSANs and vHBAs with VMM](How-to-manage-vSANs-and-vHBAs-with-VMM.md)|
|Create zones and activate any inactive zone sets. Zones connect each host or VM vHBA to a storage array.|[How to manage Virtual Fibre Channel zones and zonesets with VMM](How-to-manage-Virtual-Fibre-Channel-zones-and-zonesets-with-VMM.md)|
|Create storage array LUNs and register (unmask) them for a host, VM, or service tier as needed.|[How to manage storage LUNs for Virtual Fibre Channel with VMM](How-to-manage-storage-LUNs-for-Virtual-Fibre-Channel-with-VMM.md)|
|Create a VM template, and for each virtual Fibre Channel adapter (vHBA) that is created, specify dynamic or static WWN assignments and select the fabric classification. The fabric classification is used to connect a vHBA to a storage fabric.|[How to create a VM for Virtual Fibre Channel with VMM](How-to-create-a-VM-for-Virtual-Fibre-Channel-with-VMM.md)|
|Create a VM, select the destination host to deploy the VM to, zone a Fibre Channel array to the VM, add a disk to the VM, create a LUN, and then register (unmask) the LUN to the VM.|[How to create a VM for Virtual Fibre Channel with VMM](How-to-create-a-VM-for-Virtual-Fibre-Channel-with-VMM.md)|
|Create a service template, add VM templates to it, and for each virtual Fibre Channel adapter (vHBA) that is created, specify dynamic or static WWN assignments and select the fabric classification.|[How to create a service tier for Virtual Fibre Channel with VMM](How-to-create-a-service-tier-for-Virtual-Fibre-Channel-with-VMM.md)|
|Create and deploy the service tier, zone a Fibre Channel array to the service tier, add a disk to the service tier, create a LUN, and register (unmask) the LUN to the service tier.|[How to create a service tier for Virtual Fibre Channel with VMM](How-to-create-a-service-tier-for-Virtual-Fibre-Channel-with-VMM.md)|

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Hyper-V Virtual Fibre Channel Troubleshooting Guide](http://social.technet.microsoft.com/wiki/contents/articles/18698.hyper-v-virtual-fibre-channel-troubleshooting-guide.aspx)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



