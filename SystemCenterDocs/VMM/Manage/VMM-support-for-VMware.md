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
[!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] supports the following VMware virtualization software:

|Software|Notes|
|------------|---------|
|vCenter Server:<br /><br />-   VMware vCenter Server 6.0<br />-   VMware vCenter Server 5.8<br />-   VMware vCenter Server 5.5<br />-   VMware vCenter Server 5.1|For more information about the requirements for vCenter Server, refer to the VMware product documentation.|
|Virtual machine hosts and host clusters that run any of the following versions of VMware:<br /><br />-   VMware ESXi 6.0<br />-   VMware ESXi 5.8<br />-   VMware ESXi 5.5<br />-   VMware ESXi 5.1|The host or host clusters must be managed by a vCenter Server, which is managed by [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].|

## Supported features
When you use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to manage ESX hosts through vCenter Server, you can use the following VMware and [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] features:

|Feature|Notes|
|-----------|---------|
|**[!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] command shell**|You can use the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] command shell to manage all supported hypervisors.|
|**Placement**|When creating, deploying, or migrating VMware virtual machines, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] can use host ratings to determine virtual machine placement.<br />                This includes virtual machines deployed concurrently as part of service deployment.|
|**Services**|You can deploy [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] services to ESX hosts. **Note:** The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] service model differs from the VMware vApp model; therefore, the two types of services can coexist.However, you cannot use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to deploy vApp\-based services.|
|**Private clouds**|You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to make ESX host resources available to a private cloud.<br />You can create a private cloud from a host group that includes ESX hosts, or from a VMware resource pool.<br />You can also create quotas for the private cloud and for self\-service user roles that provide access to the private cloud. **Note:** [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not integrate with VMware vCloud.|
|**Dynamic Optimization and Power Optimization**|You can use Dynamic Optimization features with ESX hosts. For example, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] can use Live Migration to  load balance virtual machines on ESX host clusters. You can also optimize power usage by configuring [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to turn ESX hosts on and off. **Note:** For power optimization, you can use the Dynamic Optimization feature in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] or the VMware Dynamic Resource Scheduler.|
|**Migration**|You can use the following VMware transfer types to migrate virtual machines:<br /><br />-   Live Migration between hosts within cluster \(uses vMotion\)<br />-   Live Storage Migration \(uses Storage vMotion\)<br /><br />You can use the following [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] transfer types to migrate virtual machines:<br /><br />-   Network migration to and from the library **Note:**     When [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] migrates a VMware thin provisioned disk to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library, the disk becomes a thick provisioned disk.<br />-   Network migration between hosts|
|**Maintenance mode**|You can use the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console to place a  [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]\-managed ESX host into or out of maintenance mode.|
|**Library**|You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to create VMware virtual machines from VMware templates and .vmdk \(VMDK\) files.<br />You can store these resources, and the resulting virtual machines, in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library. You can also convert stored VMware virtual machines to Hyper\-V. **Important:** If you want to use VMDK files that were created in VMware Server or VMware Workstation, note that [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not support older VMDK disk types. Supported VMDK disk types include the following:<ul><li>Regular VMDK files: VMFS and monolithicFlat</li><li>VMDK files that are used to access physical disks: vmfsPassthroughRawDeviceMap</li><li>Snapshots: vmfssparse</li></ul>If you want to copy a VMDK file that uses an unsupported disk type to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library, you must use VMware conversion tools such as VMware Virtual Disk Manager to update the disk type to a supported type.|
|**Templates**|In addition to creating virtual machines, you can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to create VMware virtual machine templates and store those templates, and all the related physical files, in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library.<br /><br />You can also import templates to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library from ESX hosts or from vCenter servers. However, note that importing a template from a vCenter Server does not include importing the VMDK file; [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] in this case only imports the template metadata.|
|**Networking**|You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to deploy and manage VMware virtual machines that use both standard and distributed vSwitches and port groups.<br />However, be aware that you must use vCenter Server to configure vSwitches and port groups.<br /><br />With some configuration on the vCenter Server side, you can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] networking features such as logical networks and static IP or MAC addresses with virtual machines on ESX hosts. **Important:** To use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] networking features in this way, you must use vCenter Server to configure port groups with VLANs that correspond to the logical network sites that you have configured in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].|
|**Storage**|You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to create and manage VMware virtual machines that use<br />                VMware Paravirtual SCSI \(PVSCSI\) storage adapters. For example, when you use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to create a new virtual machine on an ESX host, you can add a SCSI adapter of type “VMware Paravirtual.” **Note:** [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not support VMware virtual machines with virtual hard disks that connect to an integrated drive electronics \(IDE\) bus.<br /><br />You can use <br />                  [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to manage VMware virtual machines that have thin provisioned disks.<br /><br />-   To create a VMware virtual machine with a thin provisioned disk, use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to create a virtual machine with a dynamic disk and deploy it to an ESX host.<br />-   If you use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to manage a VMware virtual machine with a thin provisioned disk that was created out of band, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] treats the disk as a dynamic disk<br />-   When you store a thin provisioned disk in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] converts the disk to a thick provisioned disk.<br />    This disk will remain a thick provisioned disk when you use it to create virtual machines and deploy those virtual machines to ESX hosts.<br /><br />You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to hot\-add virtual hard disks to VMware virtual machines, or hot\-remove virtual hard disks from them. **Note:** You cannot use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to configure storage resources for ESX hosts.|
|**Conversion**|You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]'s virtual to virtual \(V2V\) process to convert a VMware virtual machine to a Hyper\-V virtual machine.<br /><br />Note that [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not support VMware virtual machines with virtual hard disks that are connected to an integrated drive electronics \(IDE\) bus. Therefore, you cannot perform a V2V conversion of a VMware virtual machine that is on an IDE bus. **Note:** You can also perform V2V conversions with Microsoft Virtual Machine Converter \(MVMC\). For more information, see [Microsoft Virtual Machine Converter 3.0](http://technet.microsoft.com/library/dn873998.aspx).|
|**Performance and Resource Optimization \(PRO\)**|When you integrate [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] with Operations Manager and PRO, you can monitor ESX hosts and receive alerts from them.|

## Additional support information

-   [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] supports up to 255 GB of RAM for virtual machines that are deployed on ESX\/ESXi 4.0 hosts.

-   [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] supports up to 8 virtual CPUs \(vCPUs\) for virtual machines that are deployed on ESX\/ESXi 4.0 hosts.

-   [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] recognizes VMware fault\-tolerant virtual machines. The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console shows only the virtual machine that is designated as the primary on the vCenter Server. If there is a failure, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] recognizes the new primary.

-   You cannot use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to manage updates for ESX hosts. You must use your existing solution to update VMware ESX hosts.

-   You cannot use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to convert a bare\-metal computer to a VMware virtual machine host, or to create a cluster from ESX hosts.

-   You cannot use the Dynamic Memory feature on ESX hosts. Dynamic Memory is only supported on Hyper\-V hosts that are running an operating system that supports Dynamic Memory.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


