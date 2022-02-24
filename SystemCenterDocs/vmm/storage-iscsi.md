---
ms.assetid: 2af73b2d-621a-475e-b144-ddc03f4e2030
title: Set up a Microsoft iSCSI Target Server in the VMM 2016 storage fabric
description: This article describes how to deploy a Microsoft iSCSI Target Server in the VMM storage fabric
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Set up a Microsoft iSCSI Target Server in the VMM storage fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Microsoft iSCSI Target Server is a server role that enables a Windows server machine to function as a storage device. This article explains how to set up a Microsoft iSCSI Target Server in System Center - Virtual Machine Manager (VMM) storage.

Here's what you need to do:


1. **Install the role**: Install the iSCSI Target Server role (**Server Roles** > **File and Storage Services** > **File and iSCSI Services**) on a server that you want to add as a block storage device.
2. **Set up virtual iSCSI disks**: After installing the role you'll need to set up virtual iSCSI disks and connect to the servers you want. [Learn more](/archive/blogs/amitd/configure-windows-2012-r2-as-iscsi-target).
3. **Install the provider**: If the iSCSI Target Server runs Windows Server 2012, you must install the SMI-S provider on it. The provider is located with the setup files in \amd64\Setup\msi\iSCSITargetSMISProvider.msi, and on the VMM server in \Program Files\Microsoft System Center 2012\Virtual Machine Manager\Setup\Msi\iSCSITargetProv\iSCSITargetSMISProvider.msi. You'll need to run the .msi file on the iSCSI Target Server. If the server's running Windows Server 2012 R2 you don't need to install the provider.
4. **Add account**: Add the VMM admin account as an administrator on the server.
5. **Discover in VMM**: [Add the storage device](storage-device.md) to VMM. Select **SAN and NAS devices discovered and managed by a SMI-S provider** as the provider type, and specify the IP address or FQDN as the server. Select the account with permissions to the server as the Run As account. Add it to the required storage classification, and complete the **Add Storage Devices Wizard**.


After adding the server as a storage device under VMM management you can allocate the storage pools and LUNs to a host group and provision storage to hosts and clusters.

## PowerShell example

You can use VMM to configure the iSCSI Target Server through Windows PowerShell. This section lists some common tasks with examples of Windows PowerShell commands that you can use for those tasks. The SMI-S provider supports all management tasks through VMM.

### Manage storage on an iSCSI target server

Open PowerShell and use the cmdlets described below to manage iSCSI target server resources in VMM.



#### Add a storage provider

|Command|Purpose|
|-----------|-----------|
|`$Cred = Get-Credential`|Obtain the iSCSI Target Server local administrative credentials that are based on user name and password.<br /><br />Note that any account that is part of the Local Administrators group is sufficient.|
|`$Runas = New-SCRunAsAccount -Name "iSCSIRunas" -Credential $Cred`|Create a Run As account in VMM.|
|`Add-SCStorageProvider -Name "Microsoft iSCSI Target Provider" -RunAsAccount $Runas -ComputerName "<computername>" -AddSmisWmiProvider`|Add the storage provider.|

#### View storage properties

|Command|Purpose|
|-----------|-----------|
|`$array = Get-SCStorageArray -Name “<computername>”`|Review the storage array attributes.|
|`$array.StoragePools`|View available storage pools.|

#### Add pools from iSCSI Target Server to VMM management

|Command|Purpose|
|-----------|-----------|
|`$pool = Get-SCStoragePool -Name "MS iSCSITarget Concrete: D:"`|Get the specific storage pool to add.|
|`$class = New-SCStorageClassification -Name “gold”`|Create a storage classification, if none exists.|
|`Set-SCStorageArray -AddStoragePoolToManagement $pool -StorageArray $pool.StorageArray -StorageClassification $class`|Add the storage pool to VMM.|
|`Set-SCStoragePool -StoragePool $pool -AddVMHostGroup (Get-SCVMHostGroup -Name "All Hosts")`|Allocate the storage pool to a virtualization server group.|

#### Create a LUN

|Command|Purpose|
|-----------|-----------|
|`$LUN = New-SCStorageLogicalUnit -Name "iSCSI1" -StoragePool $pool -DiskSizeMB 1000`|Create an iSCSI logical unit number (LUN).|
|`Set-SCStorageLogicalUnit -StorageLogicalUnit $LUN -VMHostGroup (Get-SCVMHostGroup -Name "All Hosts")`|Allocate the LUN to the host group.|
|`$host = Get-SCVMhost -ComputerName <host name>`|Retrieve the properties of a host.|
|`Register-SCStorageLogicalUnit -StorageLogicalUnit $LUN -VMHost $host`|Assign the LUN to the host.|

#### Decommission resources

|Command|Purpose|
|-----------|-----------|
|`Remove-SCStorageLogicalUnit -StorageLogicalUnit $LUN`|Delete a LUN.|
|`Remove-SCStorageProvider -StorageProvider (Get-SCStorageProvider -Name "Microsoft iSCSI Target Provider")`|Remove a storage provider.|

## Next Steps

Learn about [provisioning storage](hyper-v-storage.md) for Hyper-V hosts and clusters.
