---
ms.assetid: b421d3b9-3ac5-4e02-b810-7dc8de8008c2
title: include file
description: include file to detail the new features in virtual machine manager 2019.
author:  JYOTHIRMAISURI
ms.author: V-jysur
manager:  vvithal
ms.date:  01/19/2019
ms.topic:  include
ms.prod:  system-center
ms.technology:  virtual-machine-manager
---

## New features in VMM 2019

See the following sections for detailed information about the new features/feature updates supported in VMM 2019.

## Storage

### Storage DO
This feature helps in preventing Cluster Shared Volumes (CSV) from becoming full due to expansion/new VHDs placed on the CSV. You can now set a threshold value to trigger a warning when free storage space in the CSV falls below the threshold during a new disk placement or auto migration of VHDs to other CSVs in the cluster. [Learn more](../vmm/vm-optimization.md).

### Support for storage health monitoring
Storage health monitoring helps you to monitor the health and operational status of storage pool, LUNs, and physical disks in the VMM fabric.

You can monitor the storage health in the **Fabric** page of VMM console. [Learn more](../vmm/manage-storage.md).


## Networking

### Configuration of SLB VIPs through VMM service templates
SDN in Windows 2016 can use Software Load Balancing (SLB) to evenly distribute network traffic among workloads managed by service provider and tenants. VMM 2016 currently supports deployment of  SLB Virtual IPs (VIPs) using power shell.

With VMM 2019, VMM supports configuration of SLB VIPs while deploying multi-tier application by using the service templates. [Learn more](../vmm/sdn-configure-slb-vip.md).

### Configuration of encrypted VM networks through VMM

VMM 2019 supports encryption of VM networks. Using the new encrypted networks feature, end-to-end encryption can be easily configured on VM networks by using the network controller (NC). This encryption prevents the traffic between two VMs on the same network and same subnet, from being read and manipulated.

The control of encryption is at the subnet level and encryption can be enabled/disabled for each subnet of the VM network. [Learn more](../vmm/sdn-encrypt-networks.md).

### Support for configuring layer 3 forwarding gateway using VMM console

L3 forwarding enables connectivity between the physical infrastructure in the datacenter and the virtualized infrastructure in the Hyper-V network virtualization cloud. Earlier versions of VMM supported the Layer 3 gateway configuration through PowerShell.

In VMM 2019, you can configure Layer 3 forwarding gateway using the VMM console. [Learn more](../vmm/sdn-route-network-traffic.md#configure-l3-forwarding).

### Support for Static MAC address on VMs deployed on a VMM cloud

This feature allows you to set static MAC address on VMs deployed on a cloud. You can also change the MAC address from static to dynamic and vice versa. [Learn more](../vmm/provision-vms.md).

## Azure Integration

### VM update management through VMM using Azure Automation Subscription
VMM 2019 is introducing the possibility of patching and updating on-prem VMs (managed by VMM) by integrating VMM with azure automation subscription. [Learn more](../vmm/vms-manage-azure-ad-and-region-specific.md).

### Support for new RBAC Role
In a scenario where enterprises want to create a user role for troubleshooting,  it is necessary that the user has access to all the VMs so the user can make any required changes on the VMs to resolve the issue. There is also a need for the user to have access to the fabric to identify the root cause for the issue. However, for security reasons, this user should not be given the privileges to make any changes on the fabric (such as add storage, add hosts etc).

The current RBAC in VMM does not have a role defined for this persona and the existing roles of Delegated Admin and Fabric admin have too little or more than necessary permissions to perform just troubleshooting.
To address this issue, VMM 2019 supports a new role called **Virtual Machine Administrator**. The user of this role has Read and Write access to all VMs but read-only access to the fabric. [Learn more](../vmm/account-user-role.md).

### Support for Group Managed Service Account as VMM service account

Group Managed Service Account (gMSA) helps improve the security posture and provides convenience through automatic password management, simplified service principle name (SPN) management, and the ability to delegate the management to other administrators.

VMM 2019 supports the use of gMSA for **Management server service account**. [Learn more](../vmm/install.md).

> [!NOTE]

> The following features/feature updates were introduced in VMM 1807.

## Storage

### Supports selection of CSV for placing a new VHD

VMM 1807 allows you to select a cluster shared volumes (CSV) for placing a new virtual hard disc (VHD).

In earlier versions of VMM, a new VHD on a virtual machine (VM), by default, is placed on the same CSV where the earlier VHDs associated with the VM are placed, there was no option to choose a different CSV/ folder. In case of any issues related to the CSV, such as storage full or over commitment, users had to migrate the VHD, only after deploying the VHD.

With VMM 1807, you can now  choose any location to place the new disc. You can manage this disc easily, based on the storage availability of CSVs. [Learn more](https://technet.microsoft.com/library/cc956004.aspx).

## Networking

### Display of LLDP information for networking devices
 VMM 1807 supports Link Layer Discovery Protocol (LLDP). You can now view network device properties and capabilities information of the hosts from VMM. Host operating system must be Windows 2016 or higher.

 DataCenterBridging and DataCenterBridging-LLDP-Tools features have been enabled on hosts to fetch the LLDP properties.  [Learn more](../vmm/hyper-v-network.md).

### Convert SET switch to logical switch
 VMM 1807 allows you to convert a switch embedded teaming (SET) switch to logical switch by using the VMM console. In earlier versions, this feature was supported only through PowerShell script. [Learn more](../vmm/network-switch.md).

### VMware host management
VMM 1807 supports VMware ESXi v6.5 servers in VMM fabric. This support facilitates the administrators with  additional  flexibility in managing multiple hypervisors in use. [Learn more](../vmm/system-requirements.md#vmware-servers-in-the-vmm-fabric) about the additional details of supported vmware server versions.

### Support for S2D cluster update

VMM 1807 supports update of an S2D host or a cluster. You can update individual S2D hosts or clusters against the baselines configured in windows server update services (WSUS). [Learn more](../vmm/hyper-v-update.md).

## Others

### Support for SQL 2017
VMM 1807 supports SQL 2017. You can upgrade SQL 2016 to 2017.

> [!NOTE]

> The following features/feature updates were introduced in VMM 1801.

## Compute

### Nested virtualization
VMM  supports Nested Virtualization feature that allows you to run Hyper-V inside a Hyper-V virtual machine. In other words, with nested virtualization, a Hyper-V host itself can be virtualized. Nested virtualization can be enabled out-of-band by using PowerShell and Hyper-V host configuration.

You can leverage this functionality to reduce your infrastructure expense for development, test, demo, and training scenarios. This feature also allows you to use third- party virtualization management products with Microsoft hypervisor.

You can enable or disable the nested virtualization feature using SCVMM 1801. You can configure the VM as a Host in VMM and perform host operations from VMM on this VM. For example, VMM dynamic optimization considers a nested VM host for placement.  [Learn more](../vmm/vm-nested-virtualization.md).


### Migration of VMware VM (EFI firmware-based VM) to Hyper-V VM

The current VMM migration for VMware VMs to Hyper-V only supports migration of BIOS-based VMs.

VMM 1801 release enables migration of EFI based VMware VMs to Hyper-V generation 2 VMs. VMware VMs that you migrate to Microsoft Hyper-V platform can take advantage of the Hyper-V generation 2 features.

As part of this release, the **Convert Virtual machine** wizard enables the VM migration based on the firmware type (BIOS or EFI), selects and defaults the Hyper-V VM generation appropriately: [Learn more](../vmm/vm-convert-vmware.md).

1.	BIOS-based VMs are migrated to Hyper-V VM generation 1.
2.	EFI-based VMs are migrated to Hyper-V VM generation 2.

We have also made improvements in the VMWare VM conversion process that makes the conversion up to 50% faster.

### Performance improvement in host refresher

The VMM 1801 host refresher has undergone certain updates for performance improvement.

With these updates, in scenarios where the organization is managing large number of hosts and VMs with checkpoints – you would be able to observe significant and noticeable improvements in the performance of the job.

In our lab with VMM instances managing 20 hosts - each host managing 45-100 VMs, we have measured up to 10X performance improvement.

### Enhanced console session in VMM

Console connect in VMM provides an alternative way to remote desktop to connect to the VM. This is most useful when the VM does not have any network connectivity or want to change network configuration that could break the network connectivity. Currently, the current console connect in VMM supports only basic session where clipboard text can only be pasted through Type Clipboard Text menu option.

VMM 1801 supports enhanced console session that enables **Cut (Ctrl + X)**, **Copy (Ctrl + C)** and **Paste (Ctrl + V)** operations on the ANSI text and files available on the clipboard, thereby copy/paste commands for text and files are possible from and to the VM. [Learn more](../vmm/enhanced-console-session.md).

## Storage

### Improvement in VMM storage QoS
Storage Quality of Service (SQoS) provides a way to centrally monitor and manage storage performance for virtual machines using Hyper-V and the Scale-Out File Server (SOFS) roles. The feature automatically improves storage resource fairness between multiple VMs using the same cluster and allows policy-based performance goals.

VMM 1801 supports the following improvements in SQoS:

- Extension of SQoS support beyond S2D - You can now assign storage QoS policies to storage area networks (SAN). [Learn more](../vmm/qos-storage-clusters.md).
- Support for VMM private cloud - storage QoS policies can now be consumed by the VMM cloud tenants. [Learn more](../vmm/cloud-create.md).
- Availability of storage QoS policies as templates - You can set storage QoS policies through VM templates. [Learn more](../vmm/library-vm-templates.md).


## Networking

### Configuration of guest clusters in SDN through VMM

With the advent of the software defined network (SDN), in Windows Server 2016 and System Center 2016, the configuration of guest clusters has undergone some change.

With the introduction of the SDN, VMs which are connected to the virtual network using SDN are only permitted to use the IP address that the network controller assigns for communication. The SDN design is inspired by Azure networking design, supports the floating IP functionality through the Software Load Balancer (SLB), like Azure networking.

VMM 1801 release also supports the floating IP functionality through the Software Load Balancer (SLB) in the SDN scenarios. VMM 1801 supports guest clustering through an Internal Load Balancer (ILB) VIP. The ILB uses probe ports, which are created on the guest cluster VMs to identify the active node. At any given time, the probe port of only the active node responds to the ILB and all the traffic directed to the VIP is routed to the active node.
. [Learn more](../vmm/sdn-guest-clusters.md).

### Configuration of  SLB VIPs through VMM service templates
SDN in Windows 2016 can use Software Load Balancing (SLB) to evenly distribute network traffic among workloads managed by service provider and tenants. VMM 2016 currently supports deployment of  SLB Virtual IPs (VIPs) using power shell.

With VMM 1801, VMM supports configuration of SLB VIPs while deploying multi-tier application by using the service templates. [Learn more](../vmm/sdn-configure-slb-vip.md).

### Configuration of encrypted VM networks through VMM

VMM 1801 supports encryption of VM networks. Using the new encrypted networks feature, end-to-end encryption can be easily configured on VM networks by using the Network Controller (NC). This encryption prevents traffic between two VMs on the same network and same subnet, from being read and manipulated.

The control of encryption is at the subnet level and encryption can be enabled/disabled for each subnet of the VM network. [Learn more](../vmm/sdn-encrypt-networks.md).

## Security

### Support to Linux shielded VM
Windows Server 2016 introduced the concept of a shielded VM for Windows OS-based VMs. Shielded VMs provide protection against malicious administrator actions both when VM’s data is at rest or an untrusted software is running on Hyper-V hosts.

With Windows Server 1709, Hyper-V introduces support for provisioning Linux shielded VMs and the same has been extended to VMM 1801. [Learn more](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template).

### Configuration of fallback HGS
Being at the heart of providing attestation and key protection services to run shielded VMs on Hyper-V hosts, the host guardian service (HGS) should operate even in situations of disaster. Windows Server 1709 added support for fallback HGS.

Using VMM 1801, a guarded host can be configured with a primary and a secondary pair of HGS URLS (an attestation and key protection URI). This capability enables scenarios such as guarded fabric deployments spanning two data centers for disaster recovery purposes, HGS running as shielded VMs etc.

The primary HGS URLs will always be used in favor of the secondary.  If the primary HGS fails to respond after the appropriate timeout and retry count, the operation will be reattempted against the secondary.  Subsequent operations will always favor the primary; the secondary will only be used when the primary fails.
[Learn more](../vmm/guarded-fallback-hgs.md).

## Azure Integration

### Management of Azure Resource Manager-based and region-specific Azure subscriptions

Currently, the VMM Azure plugin supports only classic virtual machines (VMs) and public Azure regions.

VMM 1801 supports management of Azure Resource Manager based VMs, Azure Active Directory (AD) based authentication that is created by using the new Azure portal and region-specific Azure subscriptions (namely, Germany, China, US Government Azure regions). [Learn more](../vmm/vms-manage-azure-ad-and-region-specific.md).
