---
title: How to configure an iSCSI Target Server with Windows PowerShell and VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91c5dd2a-550b-4884-9d3a-b935c428ead7
---
# How to configure an iSCSI Target Server with Windows PowerShell and VMM
You can use VMM to configure the iSCSI Target Server through Windows PowerShell. This section lists some common tasks with examples of Windows PowerShell commands that you can use for those tasks. The SMI\-S provider supports all management tasks through VMM.

### To manage storage on an iSCSI Target Server

1.  To open the VMM PowerShell interface, use the Windows PowerShell menu, as shown in the following illustration.

    ![](Image/VMMiSCSI5.gif)

2.  You can use the following Windows PowerShell cmdlets to manage iSCSI Target Server resources. VMM.

    -   **Add a storage provider:**

        |Command|Purpose|
        |-----------|-----------|
        |`$Cred = Get-Credential`|Obtain the iSCSI Target Server local administrative credentials that are based on user name and password.<br /><br />Note that any account that is part of the Local Administrators group is sufficient.|
        |`$Runas = New-SCRunAsAccount -Name "iSCSIRunas" -Credential $Cred`|Create a Run As account in VMM.|
        |`Add-SCStorageProvider -Name "Microsoft iSCSI Target Provider" -RunAsAccount $Runas -ComputerName "<computername>" -AddSmisWmiProvider`|Add the storage provider.|

    -   **View storage properties:**

        |Command|Purpose|
        |-----------|-----------|
        |`$array = Get-SCStorageArray -Name “<computername>”`|Review the storage array attributes.|
        |`$array.StoragePools`|View available storage pools.|

    -   **Add pools from iSCSI Target Server to VMM management:**

        |Command|Purpose|
        |-----------|-----------|
        |`$pool = Get-SCStoragePool -Name "MS iSCSITarget Concrete: D:"`|Get the specific storage pool to add.|
        |`$class = New-SCStorageClassification -Name “gold”`|Create a storage classification, if none exists.|
        |`Set-SCStorageArray -AddStoragePoolToManagement $pool -StorageArray $pool.StorageArray -StorageClassification $class`|Add the storage pool to VMM.|
        |`Set-SCStoragePool -StoragePool $pool -AddVMHostGroup (Get-SCVMHostGroup -Name "All Hosts")`|Allocate the storage pool to a virtualization server group.|

    -   **Create a LUN:**

        |Command|Purpose|
        |-----------|-----------|
        |`$LUN = New-SCStorageLogicalUnit -Name "iSCSI1" -StoragePool $pool -DiskSizeMB 1000`|Create an iSCSI logical unit number \(LUN\).|
        |`Set-SCStorageLogicalUnit -StorageLogicalUnit $LUN -VMHostGroup (Get-SCVMHostGroup -Name "All Hosts")`|Allocate the LUN to the host group.|
        |`$host = Get-SCVMhost -ComputerName <host name>`|Retrieve the properties of a host.|
        |`Register-SCStorageLogicalUnit -StorageLogicalUnit $LUN -VMHost $host`|Assign the LUN to the host.|

    -   **Decommission resources:**

        |Command|Purpose|
        |-----------|-----------|
        |`Remove-SCStorageLogicalUnit -StorageLogicalUnit $LUN`|Delete a LUN.|
        |`Remove-SCStorageProvider -StorageProvider (Get-SCStorageProvider -Name "Microsoft iSCSI Target Provider")`|Remove a storage provider.|

## See Also
[Configuring iSCSI Target Server and the SMI-S Provider in VMM](Configuring-iSCSI-Target-Server-and-the-SMI-S-Provider-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


