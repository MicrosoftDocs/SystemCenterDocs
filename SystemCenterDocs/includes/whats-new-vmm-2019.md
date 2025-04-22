---
ms.assetid: b421d3b9-3ac5-4e02-b810-7dc8de8008c2
title: include file
description: This include file describes the new features in Virtual Machine Manager 2019, 2019 UR1, UR2, UR3, UR4, and UR5.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date:  12/18/2024
ms.topic:  include
ms.service: system-center
ms.subservice: virtual-machine-manager
---

## New features in VMM 2019

The following sections introduce the new features in Virtual Machine Manager (VMM) 2019.

### Compute

#### Cluster rolling upgrade for S2D clusters

System Center 2019 Virtual Machine Manager supports a rolling upgrade of a Storage Spaces Direct (S2D) host cluster from Windows Server 2016 to Windows Server 2019. For more information, see [Perform a rolling upgrade](../vmm/hyper-v-rolling-upgrade.md).

#### Support for deduplication for ReFS volume

VMM 2019 supports deduplication for ReFS volume on the Windows Server 2019 hyper-converged cluster and Scale-Out File Server. For more information, see [Add storage to Hyper-V hosts and clusters](../vmm/hyper-v-storage.md).

### Storage

#### Storage dynamic optimization

This feature helps to prevent cluster shared storage (CSV and file shares) from becoming full due to expansion or new virtual hard disks (VHDs) being placed on the cluster shared storage. You can now set a threshold value to trigger a warning when free storage space in the cluster shared storage falls below the threshold. This situation might occur during a new disk placement. It also might occur when VHDs are automigrated to other shared storage in the cluster. For more information, see [Dynamic optimization](../vmm/vm-optimization.md#dynamic-optimization).

#### Support for storage health monitoring

Storage health monitoring helps you to monitor the health and operational status of storage pools, LUNs, and physical disks in the VMM fabric.

You can monitor the storage health on the **Fabric** page of the VMM console. For more information, see [Set up the VMM storage fabric](../vmm/manage-storage.md).


### Networking

#### Configuration of SLB VIPs through VMM service templates

Software-defined networks (SDNs) in Windows 2016 can use software load balancing (SLB) to evenly distribute network traffic among workloads managed by service providers and tenants. VMM 2016 currently supports deployment of SLB virtual IPs (VIPs) by using PowerShell.

With VMM 2019, VMM supports configuration of SLB VIPs while deploying multitier applications by using the service templates. For more information, see [Configure SLB VIPs through VMM service templates](../vmm/sdn-configure-slb-vip.md).

#### Configuration of encrypted VM networks through VMM

VMM 2019 supports encryption of VM networks. Using the new encrypted networks feature, end-to-end encryption can be easily configured on VM networks by using the network controller. This encryption prevents the traffic between two VMs on the same network and the same subnet from being read and manipulated.

The control of encryption is at the subnet level. Encryption can be enabled or disabled for each subnet of the VM network. For more information, see [Configure encrypted networks in SDN using VMM](../vmm/sdn-encrypt-networks.md).

#### Support for configuring a Layer 3 forwarding gateway by using the VMM console

Layer 3 (L3) forwarding enables connectivity between the physical infrastructure in the datacenter and the virtualized infrastructure in the Hyper-V network virtualization cloud. Earlier versions of VMM supported the Layer 3 gateway configuration through PowerShell.

In VMM 2019, you can configure a Layer 3 forwarding gateway by using the VMM console. For more information, see [Configure L3 forwarding](../vmm/sdn-route-network-traffic.md#tab/configure-l3-forwarding-1).

#### Support for a static MAC address on VMs deployed on a VMM cloud

With this feature, you can set a static MAC address on VMs deployed on a cloud. You can also change the MAC address from static to dynamic and vice versa for the already-deployed VMs. For more information, see [Provision virtual machines in the VMM fabric](../vmm/provision-vms.md).

### Azure integration

#### VM update management through VMM by using an Azure Automation subscription

VMM 2019 introduces the possibility of patching and updating on-premises VMs (managed by VMM) by integrating VMM with an Azure Automation subscription. For more information, see [Manage VMs](../vmm/vms-manage-azure-ad-and-region-specific.md).

#### New RBAC role: Virtual Machine Administrator

In a scenario where enterprises want to create a user role for troubleshooting, the user needs access to all the VMs. In this way, the user can make any required changes on the VMs to resolve a problem. There's also a need for the user to have access to the fabric to identify the root cause for a problem. For security reasons, this user shouldn't be given privileges to make any changes on the fabric like adding storage or hosts.

The current role-based access control (RBAC) in VMM doesn't have a role defined for this persona. The existing roles of Delegated Admin and Fabric Admin have too little or more than necessary permissions to perform troubleshooting.

To address this issue, VMM 2019 supports a new role called **Virtual Machine Administrator**. The user of this role has Read and Write access to all VMs but Read-only access to the fabric. For more information, see [Set up user roles in VMM](../vmm/account-user-role.md).

#### Support for group Managed Service Account as a VMM service account

The group Managed Service Account (gMSA) helps improve the security posture. It provides convenience through automatic password management, simplified service principle name management, and the ability to delegate the management to other administrators.

VMM 2019 supports the use of gMSA for Management server service account. For more information, see [Install VMM](../vmm/install.md).

> [!NOTE]
> The following features or feature updates were introduced in VMM 1807 and are included in VMM 2019.

## Features included in VMM 2019 - introduced in VMM 1807

### Storage

#### Supports selection of CSV for placing a new VHD

With VMM, you can select cluster shared volumes (CSVs) for placing a new VHD.

In earlier versions of VMM, by default a new VHD on a VM is placed on the same CSV where the earlier VHDs associated with the VM are placed. There was no option to choose a different CSV/ folder. In case of any problems related to the CSV, such as storage that's full or over commitment, users had to migrate the VHD, but only after they deployed the VHD.

With VMM 1807, you can now choose any location to place the new disk. You can manage this disk easily, based on the storage availability of CSVs. For more information, see [Add a virtual hard disk to a virtual machine](/previous-versions/system-center/virtual-machine-manager-2008-r2/cc956004(v=technet.10)).

### Networking

#### Display of LLDP information for networking devices

 VMM supports the Link Layer Discovery Protocol (LLDP). You can now view network device properties and capabilities information of the hosts from VMM. The host operating system must be Windows 2016 or higher.

 DataCenterBridging and DataCenterBridging-LLDP-Tools features have been enabled on hosts to fetch the LLDP properties. For more information, see [Set up networking for Hyper-V hosts and clusters in the VMM fabric](../vmm/hyper-v-network.md).

#### Convert a SET switch to a logical switch

 You can convert a switch embedded teaming (SET) switch to a logical switch by using the VMM console. In earlier versions, this feature was supported only through PowerShell script. For more information, see [Create logical switches](../vmm/network-switch.md).

#### VMware host management

VMM supports VMware ESXi v6.5 servers in VMM fabric. This support gives administrators additional flexibility in managing multiple hypervisors in use. For more information about supported VMware server versions, see [System requirements](../vmm/system-requirements.md#vmware-servers-in-the-vmm-fabric).

#### Support for S2D cluster update

VMM supports the update of an S2D host or a cluster. You can update individual S2D hosts or clusters against the baselines configured in Windows Server Update Services. For more information, see [Update Hyper-V hosts and clusters](../vmm/hyper-v-update.md).

### Others

#### Support for SQL Server 2017

VMM supports SQL Server 2017. You can upgrade SQL Server 2016 to SQL Server 2017.

> [!NOTE]
> The following features or feature updates were introduced in VMM 1801 and are included in VMM 2019.

## Features included in VMM 2019 - introduced in VMM 1801

### Compute

#### Nested virtualization

VMM supports a nested virtualization feature that you can use to run Hyper-V inside a Hyper-V virtual machine. In other words, with nested virtualization, a Hyper-V host itself can be virtualized. Nested virtualization can be enabled out-of-band by using PowerShell and Hyper-V host configuration.

You can use this functionality to reduce your infrastructure expense for development, test, demo, and training scenarios. With this feature, you can also use non-Microsoft virtualization management products with Hyper-V.

You can enable or disable the nested virtualization feature by using VMM. You can configure the VM as a host in VMM and perform host operations from VMM on this VM. For example, VMM dynamic optimization considers a nested VM host for placement. For more information, see [Configure a nested VM as a host](../vmm/vm-nested-virtualization.md).


#### Migration of VMware VM (EFI firmware-based VM) to Hyper-V VM

The current VMM migration for VMware VMs to Hyper-V only supports migration of BIOS-based VMs.

VMM enables migration of EFI-based VMware VMs to Hyper-V generation 2 VMs. VMware VMs that you migrate to Microsoft Hyper-V platform can take advantage of the Hyper-V generation 2 features.

As part of this release, the **Convert Virtual Machine** wizard enables the VM migration based on the firmware type (BIOS or EFI). It selects and defaults the Hyper-V VM generation appropriately. For more information, see [Convert a VMware VM to Hyper-V in the VMM fabric](../vmm/vm-convert-vmware.md). For example:

* BIOS-based VMs are migrated to Hyper-V VM generation 1.
* EFI-based VMs are migrated to Hyper-V VM generation 2.

We've also made improvements in the VMware VM conversion process that makes the conversion up to 50% faster.

#### Performance improvement in host refresher

 VMM host refresher has undergone certain updates for performance improvement.

With these updates, in scenarios where an organization manages a large number of hosts and VMs with checkpoints, you can observe significant and noticeable improvements in the performance of the job.

In our lab with VMM instances managing 20 hosts, and each host managing 45 to 100 VMs, we've measured up to 10 times performance improvement.

#### Enhanced console session in VMM

The console connect capability in VMM provides an alternative way to connect to the VM via remote desktop. This method is most useful when the VM doesn't have any network connectivity or when you want to change to a network configuration that could break the network connectivity. Currently, the console connect capability in VMM supports only a basic session where clipboard text can be pasted only by using the **Type Clipboard Text** menu option.

VMM supports an enhanced console session that enables **Cut (Ctrl + X)**, **Copy (Ctrl + C)**, and **Paste (Ctrl + V)** operations on the ANSI text and files available on the clipboard. As a result, **Copy** and **Paste** commands for text and files are possible from and to the VM. For more information, see [Enable enhanced console session in VMM](../vmm/enhanced-console-session.md).

### Storage

#### Improvement in VMM storage QoS

Storage Quality of Service (QoS) provides a way to centrally monitor and manage storage performance for virtual machines by using Hyper-V and the Scale-Out File Server roles. The feature automatically improves storage resource fairness between multiple VMs by using the same cluster. It also allows policy-based performance goals.

VMM supports the following improvements in storage QoS:

- **Extension of storage QoS support beyond S2D:** You can now assign storage QoS policies to storage area networks (SANs). For more information, see [Manage storage QoS for clusters](../vmm/qos-storage-clusters.md).
- **Support for VMM private clouds:** Storage QoS policies can now be consumed by the VMM cloud tenants. For more information, see [Create a private cloud](../vmm/cloud-create.md).
- **Availability of storage QoS policies as templates:** You can set storage QoS policies through VM templates. For more information, see [Add VM templates to the VMM library](../vmm/library-vm-templates.md).


### Networking

#### Configuration of guest clusters in SDN through VMM

With the advent of the software-defined network in Windows Server 2016 and System Center 2016, the configuration of guest clusters has undergone some change.

With the introduction of the SDN, VMs that are connected to the virtual network by using SDN are only permitted to use the IP address that the network controller assigns for communication. The SDN design is inspired by Azure networking design and supports the floating IP functionality through the software load balancer (SLB) like Azure networking.

VMM also supports the floating IP functionality through the SLB in the SDN scenarios. VMM 1801 supports guest clustering through an internal load balancer (ILB) VIP. The ILB uses probe ports, which are created on the guest cluster VMs to identify the active node. At any given time, the probe port of only the active node responds to the ILB. Then all the traffic directed to the VIP is routed to the active node. For more information, see [Configure guest clusters in SDN through VMM](../vmm/sdn-guest-clusters.md).

#### Configuration of SLB VIPs through VMM service templates

SDN in Windows 2016 can use SLB to evenly distribute network traffic among workloads managed by service provider and tenants. VMM 2016 currently supports deployment of SLB VIPs by using PowerShell.

 VMM supports configuration of SLB VIPs when you deploy multitier applications by using the service templates. For more information, see [Configure SLB VIPs through VMM service templates](../vmm/sdn-configure-slb-vip.md).

#### Configuration of encrypted VM networks through VMM

VMM supports encryption of VM networks. Using the new encrypted networks feature, end-to-end encryption can be easily configured on VM networks by using the network controller. This encryption prevents traffic between two VMs on the same network and same subnet from being read and manipulated.

The control of encryption is at the subnet level. Encryption can be enabled or disabled for each subnet of the VM network. For more information, see [Configure encrypted networks in SDN using VMM](../vmm/sdn-encrypt-networks.md).

### Security

#### Support to Linux shielded VMs

Windows Server 2016 introduced the concept of a shielded VM for Windows OS-based VMs. Shielded VMs protect against malicious administrator actions. They provide protection when the VM's data is at rest or when untrusted software runs on Hyper-V hosts.

With Windows Server 1709, Hyper-V introduces support for provisioning Linux shielded VMs. The same support is now extended to VMM. For more information, see [Create a Linux shielded VM template disk](/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template).

#### Configuration of fallback HGS

The host guardian service (HGS) provides attestation and key protection services to run shielded VMs on Hyper-V hosts. It should operate even in situations of disaster. Windows Server 1709 added support for fallback HGS.

Using VMM, a guarded host can be configured with a primary and a secondary pair of HGS URLS (an attestation and key protection URI). This capability enables scenarios such as guarded fabric deployments that span two datacenters for disaster recovery purposes and HGS running as shielded VMs.

The primary HGS URLs are always used in favor of the secondary HGS URLs. If the primary HGS fails to respond after the appropriate timeout and retry count, the operation is reattempted against the secondary HGS. Subsequent operations always favor the primary. The secondary is used only when the primary fails.
For more information, see [Configure HGS fallback URLs in VMM](../vmm/guarded-fallback-hgs.md).

### Azure integration

#### Management of Azure Resource Manager-based and region-specific Azure subscriptions

Currently, the VMM Azure plug-in supports only classic VMs and global Azure regions.

VMM 1801 supports management of:

* Azure Resource Manager-based VMs.
* Microsoft Entra ID-based authentication that's created by using the new Azure portal.
* Region-specific Azure subscriptions, namely, Germany, China, and US Government Azure regions.

For more information, see [Manage VMs](../vmm/vms-manage-azure-ad-and-region-specific.md).

## New features in VMM 2019 UR1

The following sections introduce the new features or feature updates supported in VMM 2019 Update Rollup 1 (UR1).

For problems fixed in UR1, and the installation instructions for UR1, see [the KB article](https://support.microsoft.com/help/4533411).

### Compute

#### Support for management of replicated library shares

Large enterprises usually have multisite datacenter deployments to cater to various offices across the globe. These enterprises typically have a locally available library server to access files for VM deployment rather than accessing the library shares from a remote location. This arrangement is to avoid any network-related problems users might experience. But library files must be consistent across all the datacenters to ensure uniform VM deployments. To maintain uniformity of library contents, organizations use replication technologies.

VMM now supports the management of library servers, which are replicated. You can use any replication technologies, such as DFSR, and manage the replicated shares through VMM. For more information, see [Manage replicated library shares](../vmm/library-resources.md#manage-replicated-library-shares).

### Storage

#### Configuration of DCB settings on S2D clusters

Remote Direct Memory Access (RDMA) and data center bridging (DCB) help to achieve a similar level of performance and losslessness in an Ethernet network as in fiber channel networks.

VMM 2019 UR1 supports configuration of DCB on S2D clusters.

>[!NOTE]
>You must configure the DCB settings consistently across all the hosts and the fabric network (switches). A misconfigured DCB setting in any one of the host or fabric devices is detrimental to the S2D performance. For more information, see [Configure DCB settings on the S2D cluster](../vmm/s2d-hyper-converged.md#step-3-configure-dcb-settings-on-the-s2d-cluster).

### Networking

#### User experience improvements in logical networks

In VMM 2019 UR1, the user experience is enhanced for the process of creating logical networks. Logical networks are now grouped by product description based on use cases. Also, an illustration for each logical network type and a dependency graph are provided. For more information, see [Set up logical networks in the VMM 2019 UR1 fabric](../vmm/network-logical-ur1.md).

#### Additional options to enable nested virtualization

You can now enable nested virtualization while you create a new VM and deploy VMs through VM templates and service templates. In earlier releases, nested virtualization is supported only on deployed VMs. Learn more about [enabling nested virtualization](../vmm/vm-nested-virtualization.md).

### Updates to PowerShell cmdlets

VMM 2019 UR1 includes the following cmdlet updates for the respective features:

1. Configuration of DCB settings on S2D clusters

   - New cmdlet  **New-SCDCBSettings** - configures DCB settings in the S2D cluster managed by VMM.

   - New parameter **[-DCBSettings]** - specifies the DCB settings configured on the cluster, and is included in **Install-SCVMHostCluster**, **Set-SCVMHostCluster**, and **Set-SCStorageFileServer** cmdlets.


2. Additional options to enable nested virtualization

   - New parameter **[-EnableNestedVirtualization]** - enables the nested virtualization and is included in **Set-SCComputerTierTemplate** cmdlet.


For more information about these updates, see [VMM PowerShell articles](/powershell/module/virtualmachinemanager/?preserve-view=true&view=systemcenter-ps-2019).


## New features in VMM 2019 UR2

The following sections introduce the new features and feature updates supported in VMM 2019 Update Rollup 2 (UR2).

For problems fixed in VMM 2019 UR2 and installation instructions for UR2, [see the KB article](https://support.microsoft.com/help/4569533).

### Compute

#### Support for Windows Server 2012 R2 hosts

VMM 2019 UR2 supports windows server 2012 R2 hosts. For more information about the supported hosts, see [System requirements](../vmm/system-requirements.md#servers-in-the-vmm-fabric).

#### Support for ESXi 6.7 hosts

VMM 2019 UR2 supports VMware ESXi v6.7 servers in VMM fabric. This support gives additional flexibility to the administrators in managing multiple hypervisors in use. For more information about supported VMware server versions, see [System requirements](../vmm/system-requirements.md#vmware-servers-in-the-vmm-fabric).

### Networking

#### User experience improvements in creating logical switches
With VMM 2019 UR2, the user experience is enhanced for the process of creating logical switches. 2019 UR2 includes smart defaults, provides clear text explanation for various options along with visual representations, and a topology diagram for logical switch. [Learn more](../vmm/network-switch.md).

#### Support for IPv6

VMM 2019 UR2 supports IPv6 SDN deployment. [Learn more](../vmm/sdn-controller.md).

#### Provision to set affinity between virtual network adapters and physical adapters

VMM 2019 UR2 supports affinity between vNICs and pNICs. Affinity between virtual network adapters and physical adapters brings in flexibility to route network traffic across teamed pNICs. With this feature, you can increase throughput by mapping RDMA capable physical adapter with an RDMA settings-enabled vNIC. Also, you can route specific type of traffic (for example, live migration) to a higher-bandwidth physical adapter. In HCI deployment scenarios, by specifying affinity, you can use SMB multichannel to meet high throughput for SMB traffic. [Learn more](../vmm/hyper-v-network.md#set-affinity-between-vnics-and-pnics).

### Others

#### Support for SQL Server 2019
VMM 2019 RTM and later now supports SQL Server 2019.

#### Support for Linux Operating system

VMM 2019 UR2 supports Red Hat 8.0, CentOS 8, Debian 10, Ubuntu 20.04 Linux Operating systems.

### Updates to PowerShell cmdlets

VMM 2019 UR2 includes the following cmdlet updates for the respective features:

1. Update VMM certificate

   - New cmdlet **Update-SCVMMCertificate** - updates the VMM certificate on the VMM server.   


2. Set affinity between virtual network adapters and physical adapters

   - New parameter **[-PhysicalNetworkAdapterName]** - specifies the name of the physical network adapter and is included in **New-SCVirtualNetworkAdapter** and **Set-SCVirtualNetworkAdapter** cmdlets.


3. Support for IPv6

    - New parameter **[-IPv6Subnet]** - specifies an IPv6 subnet and is included in **Add-SCFabricRoleResource** cmdlet.

    - Updates to parameters in existing cmdlets:
      - IPv4 and IPv6 address separated by ‘;’ can be passed to **[-RoutingIPSubnet]** parameter in **Add-SCVMNetworkGateway** cmdlet.
      - IPv6 addresses can also be added to **[-PublicIPAddresses]** parameter in **New-SCGatewayRoleConfiguration** cmdlet.

For more information about these updates, see [VMM PowerShell articles](/powershell/module/virtualmachinemanager/?preserve-view=true&view=systemcenter-ps-2019).


## New features in VMM 2019 UR3

The following sections introduce the new features and feature updates supported in VMM 2019 Update Rollup 3 (UR3).

For problems fixed in VMM 2019 UR3, and installation instructions for UR3, [see the KB article](https://support.microsoft.com/topic/2eea517c-bd0f-dfe8-2c70-28fa4ac6b0c1).

### Compute

#### Trunk mode support for VM vNICs

VMM 2019 UR3 includes Trunk mode support for VM vNICs. Trunk mode is used by NFV/VNF applications like virtual firewalls, software load balancers, and virtual gateways to send and receive traffic over multiple vLANs. [Learn more](../vmm/vm-settings.md#support-for-trunk-mode).

#### Support for Azure Local instances

VMM 2019 UR3 includes support to add, deploy, and manage Azure Local instances in VMM. In addition to the current SKU of server operating system, VMM expands its support to Azure Local.

Azure Stack HCI, version 20H2 is the newly introduced hyper-converged infrastructure (HCI) Operating system that runs on on-premises clusters with virtualized workloads.

Most of the operations to manage Azure Local instances in VMM are similar to that of managing Windows Server clusters. [Learn more](../vmm/deploy-manage-azure-stack-hci.md).

>[!NOTE]
>Management of Azure Local *stretched* clusters is currently not supported in VMM.

### Updates to PowerShell cmdlets

VMM 2019 UR3 includes the following cmdlet updates for Trunk mode support for VM vNICs:

New parameters **[-AllowedVLanList]** and **[NativeVLanId]** are included in **New-SCVirtualNetworkAdapter** and **Set-SCVirtualNetworkAdapter** cmdlets.

For more information about these updates, see [VMM PowerShell articles](/powershell/module/virtualmachinemanager/?preserve-view=true&view=systemcenter-ps-2019).

## New features in VMM 2019 UR4

The following sections introduce the new features or feature updates supported in VMM 2019 Update Rollup 4 (UR4).

For problems fixed in UR4, and the installation instructions for UR4, see [the KB article](https://support.microsoft.com/topic/update-rollup-4-for-system-center-2019-virtual-machine-manager-045605ba-7de1-4569-bad2-9f7c6ccc42c4).

### Compute

#### Support for Windows Server 2022 and Windows 11

VMM 2019 UR4 supports Windows Server 2012 2022 and Windows 11 guest virtual machines. For more information about supported hosts, see [System requirements](/system-center/vmm/system-requirements?view=sc-vmm-2019&preserve-view=true#servers-in-the-vmm-fabric).

#### Support for Smart card sign in

VMM 2019 UR4 supports smart card sign in to connect virtual machines in enhanced session mode.

## New features in VMM 2019 UR5

The following sections introduce the new features or feature updates supported in VMM 2019 Update Rollup 5 (UR5).

For problems fixed in UR5, and the installation instructions for UR5, see the [KB article](https://support.microsoft.com/topic/update-rollup-5-for-system-center-2019-virtual-machine-manager-e40c2217-3512-4421-a429-5724d297b11e).

### Compute

#### Support for VMware vSphere 7.0, 8.0 and ESXi 7.0, 8.0

VMM 2019 UR5 supports VMware vSphere 7.0, 8.0 and ESXi 7.0, 8.0. [Learn more](/system-center/vmm/system-requirements?view=sc-vmm-2019&preserve-view=true#servers-in-the-vmm-fabric).

### Discover Arc-enabled SCVMM from VMM console

VMM 2019 UR5 allows you to discover Arc-enabled SCVMM from console and manage your Hybrid environment and perform self-service VM operations through Azure portal. [Learn more](/system-center/vmm/about-arc-enabled-system-center-virtual-machine-manager?view=sc-vmm-2019&preserve-view=true).

## New features in VMM 2019 UR6

The following sections introduce the new features or feature updates supported in VMM 2019 Update Rollup 6 (UR6).

For problems fixed in UR6, and the installation instructions for UR6, see the [KB article](https://support.microsoft.com/kb/5035468).

### Improved Arc-enabled SCVMM Discovery tab

The **Azure Arc** tab now highlights the latest feature additions to Arc-enabled SCVMM which includes support for Azure management services such as Microsoft Defender for Cloud, Azure Update Manager, Azure Monitor, Microsoft Sentinel, and more. [Learn more](https://techcommunity.microsoft.com/t5/azure-arc-blog/introducing-azure-management-capabilities-for-azure-arc-enabled/ba-p/3947253).

If you are running WS 2012 and 2012R2 host and guest operating systems, the Azure Arc blade now provides guidance to continue remaining in support state.