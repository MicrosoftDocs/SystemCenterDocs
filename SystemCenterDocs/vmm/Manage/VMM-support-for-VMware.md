---
title: VMM support for VMware
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 442f26d8-4e71-4074-a832-41ee47fd56d6
---
# VMM support for VMware
VMM supports the following VMware virtualization software:

|Software|Notes|
|------------|---------|
|vCenter Server:<br /><br />-   VMware vCenter Server 6.0<br />-   VMware vCenter Server 5.8<br />-   VMware vCenter Server 5.5<br />-   VMware vCenter Server 5.1|For more information about the requirements for vCenter Server, refer to the VMware product documentation.|
|Virtual machine hosts and host clusters that run any of the following versions of VMware:<br /><br />-   VMware ESXi 6.0<br />-   VMware ESXi 5.8<br />-   VMware ESXi 5.5<br />-   VMware ESXi 5.1|The host or host clusters must be managed by a vCenter Server, which is managed by VMM.|

## Supported features
When you use VMM to manage ESX hosts through vCenter Server, you can use the following VMware and VMM features:

|Feature|Notes|
|-----------|---------|
|**VMM command shell**|You can use the VMM command shell to manage all supported hypervisors.|
|**Placement**|When creating, deploying, or migrating VMware virtual machines, VMM can use host ratings to determine virtual machine placement.<br />                This includes virtual machines deployed concurrently as part of service deployment.|
|**Services**|You can deploy VMM services to ESX hosts. **Note:** The VMM service model differs from the VMware vApp model; therefore, the two types of services can coexist.However, you cannot use VMM to deploy vApp-based services.|
|**Private clouds**|You can use VMM to make ESX host resources available to a private cloud.<br />You can create a private cloud from a host group that includes ESX hosts, or from a VMware resource pool.<br />You can also create quotas for the private cloud and for self-service user roles that provide access to the private cloud. **Note:** VMM does not integrate with VMware vCloud.|
|**Dynamic Optimization and Power Optimization**|You can use Dynamic Optimization features with ESX hosts. For example, VMM can use Live Migration to  load balance virtual machines on ESX host clusters. You can also optimize power usage by configuring VMM to turn ESX hosts on and off. **Note:** For power optimization, you can use the Dynamic Optimization feature in VMM or the VMware Dynamic Resource Scheduler.|
|**Migration**|You can use the following VMware transfer types to migrate virtual machines:<br /><br />-   Live Migration between hosts within cluster (uses vMotion)<br />-   Live Storage Migration (uses Storage vMotion)<br /><br />You can use the following VMM transfer types to migrate virtual machines:<br /><br />-   Network migration to and from the library **Note:**     When VMM migrates a VMware thin provisioned disk to the VMM library, the disk becomes a thick provisioned disk.<br />-   Network migration between hosts|
|**Maintenance mode**|You can use the VMM console to place a  VMM-managed ESX host into or out of maintenance mode.|
|**Library**|You can use VMM to create VMware virtual machines from VMware templates and .vmdk (VMDK) files.<br />You can store these resources, and the resulting virtual machines, in the VMM library. You can also convert stored VMware virtual machines to Hyper-V. **Important:** If you want to use VMDK files that were created in VMware Server or VMware Workstation, note that VMM does not support older VMDK disk types. Supported VMDK disk types include the following:<ul><li>Regular VMDK files: VMFS and monolithicFlat</li><li>VMDK files that are used to access physical disks: vmfsPassthroughRawDeviceMap</li><li>Snapshots: vmfssparse</li></ul>If you want to copy a VMDK file that uses an unsupported disk type to the VMM library, you must use VMware conversion tools such as VMware Virtual Disk Manager to update the disk type to a supported type.|
|**Templates**|In addition to creating virtual machines, you can use VMM to create VMware virtual machine templates and store those templates, and all the related physical files, in the VMM library.<br /><br />You can also import templates to the VMM library from ESX hosts or from vCenter servers. However, note that importing a template from a vCenter Server does not include importing the VMDK file; VMM in this case only imports the template metadata.|
|**Networking**|You can use VMM to deploy and manage VMware virtual machines that use both standard and distributed vSwitches and port groups.<br />However, be aware that you must use vCenter Server to configure vSwitches and port groups.<br /><br />With some configuration on the vCenter Server side, you can use VMM networking features such as logical networks and static IP or MAC addresses with virtual machines on ESX hosts. **Important:** To use VMM networking features in this way, you must use vCenter Server to configure port groups with VLANs that correspond to the logical network sites that you have configured in VMM.|
|**Storage**|You can use VMM to create and manage VMware virtual machines that use<br />                VMware Paravirtual SCSI (PVSCSI) storage adapters. For example, when you use VMM to create a new virtual machine on an ESX host, you can add a SCSI adapter of type “VMware Paravirtual.” **Note:** VMM does not support VMware virtual machines with virtual hard disks that connect to an integrated drive electronics (IDE) bus.<br /><br />You can use <br />                  VMM to manage VMware virtual machines that have thin provisioned disks.<br /><br />-   To create a VMware virtual machine with a thin provisioned disk, use VMM to create a virtual machine with a dynamic disk and deploy it to an ESX host.<br />-   If you use VMM to manage a VMware virtual machine with a thin provisioned disk that was created out of band, VMM treats the disk as a dynamic disk<br />-   When you store a thin provisioned disk in the VMM library, VMM converts the disk to a thick provisioned disk.<br />    This disk will remain a thick provisioned disk when you use it to create virtual machines and deploy those virtual machines to ESX hosts.<br /><br />You can use VMM to hot-add virtual hard disks to VMware virtual machines, or hot-remove virtual hard disks from them. **Note:** You cannot use VMM to configure storage resources for ESX hosts.|
|**Conversion**|You can use VMM's virtual to virtual (V2V) process to convert a VMware virtual machine to a Hyper-V virtual machine.<br /><br />Note that VMM does not support VMware virtual machines with virtual hard disks that are connected to an integrated drive electronics (IDE) bus. Therefore, you cannot perform a V2V conversion of a VMware virtual machine that is on an IDE bus. **Note:** You can also perform V2V conversions with Microsoft Virtual Machine Converter (MVMC). For more information, see [Microsoft Virtual Machine Converter 3.0](http://technet.microsoft.com/library/dn873998.aspx).|
|**Performance and Resource Optimization (PRO)**|When you integrate VMM with Operations Manager and PRO, you can monitor ESX hosts and receive alerts from them.|

## Additional support information

-   VMM supports up to 255 GB of RAM for virtual machines that are deployed on ESX/ESXi 4.0 hosts.

-   VMM supports up to 8 virtual CPUs (vCPUs) for virtual machines that are deployed on ESX/ESXi 4.0 hosts.

-   VMM recognizes VMware fault-tolerant virtual machines. The VMM console shows only the virtual machine that is designated as the primary on the vCenter Server. If there is a failure, VMM recognizes the new primary.

-   You cannot use VMM to manage updates for ESX hosts. You must use your existing solution to update VMware ESX hosts.

-   You cannot use VMM to convert a bare-metal computer to a VMware virtual machine host, or to create a cluster from ESX hosts.

-   You cannot use the Dynamic Memory feature on ESX hosts. Dynamic Memory is only supported on Hyper-V hosts that are running an operating system that supports Dynamic Memory.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


