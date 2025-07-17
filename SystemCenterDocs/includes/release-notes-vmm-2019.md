---
ms.assetid: ac25266c-9def-404d-95dc-6d037fb710e4
title: Include file
description: Include file to summarize the release notes for VMM 2019.
author: jyothisuri
ms.author: jsuri
ms.date:  03/19/2024
ms.topic:  include
ms.service: system-center
ms.subservice: virtual-machine-manager
---

## VMM 2019 release notes

The following sections summarize the release notes for VMM 2019 and include the known issues and workarounds.
No known issues in VMM 2019 UR1 and UR2.

- For issues fixed in 2019 UR1, [see the KB article for UR1](https://support.microsoft.com/help/4533411/update-rollup-1-for-system-center-virtual-machine-manager-2019).
- For issues fixed in 2019 UR2, [see the KB article for UR2](https://support.microsoft.com/help/4569533).
- For issues fixed in 2019 UR3, [see the KB article for UR3](https://support.microsoft.com/kb/5001835).
- For issues fixed in 2019 UR4, [see the KB article for UR4](https://support.microsoft.com/kb/5014156).
- For issues fixed in 2019 UR5, [see the KB article for UR5](https://support.microsoft.com/kb/5024282).
- For issues fixed in 2019 UR6, [see the KB article for UR6](https://support.microsoft.com/kb/5035468).

## Removal of cluster node fails with CleanUpDisks flag

 **Description**: When you remove a cluster node from Windows Server 2019 S2D cluster, with a CleanUpDisks flag, the removal fails with **Could not get the specified instance MSFT_StorageJob** error, in the following scenarios.

  - The storage capacity is inadequate in the remaining servers to accommodate all the volumes.

  - There aren't enough fault domains to provide the resiliency of the volume.  

**Workaround**: Ensure the following:

-  Adequate storage capacity is available in the remaining servers to accommodate all the volumes

-  Enough fault domains are available to provide the resiliency of your volumes.  

## Addition of storage device having SMI-S management interface fails

**Description**: Addition of storage device having SMI-S management interface fails with the error *Registration of storage provider failed with error code WsManMIInvokeFailed* when System Center Virtual Machine Manager (VMM) 2019 is installed on Windows Server 2019.  

**Workaround**: VMM depends on the *Windows Standards-Based Storage Management* service to manage the storage devices using SMI-S. Ensure that the service is started before trying to add the storage device.  

## Windows Server 2019 doesn't support HNVv1 networks

**Description**: Windows Server 2019 doesn't support HNVv1. If HNVv1 is currently in use, then the cluster that is utilizing HNVv1 shouldn't be upgraded to Windows Server 2019 using Cluster Rolling Upgrade.

**Workaround**: Migrate out of HNVv1 to SDNv2 on Windows Server 2016 before using Cluster Rolling upgrade to Windows Server 2019.

## Latest accessibility fixes in Console aren't available

**Description**: Latest accessibility fixes in Console might not be available when you use .NET 4.7 while installing the VMM console.

**Workaround**: We recommend you to use .NET 4.8. For detailed information on .NET 4.8 migration, see [the article on .NET migration
 ](/dotnet/framework/migration-guide/).    

## Backend adapter connectivity for SLB MUX doesn't work as expected

**Description**: Backend adapter connectivity of SLB MUX might not work as expected after the migration of virtual machine (VM).

**Workaround**: Users scale in/scale out in the SLB MUX VM as a workaround.

## Cluster Rollup Upgrade fails

**Description**: Cluster rollup upgrade (CRU) fails during the *Connect Hyper-V host to storage arrays* stage, if the Windows Server 2019 Virtual Hard Disk (VHD) in library server, used as the computer profile for redeploying the operating system (OS) isn't installed with the latest updates.

**Workaround**: To resolve this error, install all the pending updates on the VHD and restart the CRU job.

To avoid this issue, prior to CRU triggering, ensure to install the latest OS updates on the VHD that you want to use for CRU.  

## Storage Dynamic Optimization doesn't trigger VHD migration even when optimization criteria are met

**Description**: Storage Dynamic Optimization (DO) should trigger the VHD migration between Clustered Shared Volumes (CSV), when the free storage space in one of the CSVs falls below the disk space threshold set in the Dynamic Optimization page, and the aggressiveness criteria are met. However, in some cases, the VHDs might not be migrated even if all other Storage DO conditions are met.

**Workaround**: To ensure Storage migration is triggered, do the following:
1.	Check the *HostVolumeID* using *Get-SCStorageVolume* cmdlet. If the *HostVolumeID* returns Null for the volume, refresh the VM and perform Storage DO again.
2.	Check the *DiskSpacePlacementLevel* of the host group using the *Get-SCHostResever* cmdlet. Set the *DiskSpacePlacementLevel* value that is equal to the value of disk space as in *Host Reserve* settings, in the Dynamic Optimization wizard.

## Storage Dynamic Optimization disk performs multiple back and forth VHD migrations

**Description**: If there's a mismatch of disk space warning levels between host groups having the same file share, it can result in multiple migrations, to and from that file share, and might impact storage DO performance.

**Workaround**: We recommend that you don't do a file share across different clusters where storage dynamic optimization is enabled.

## Performance monitoring for VMM server fails with *Access denied* event error

**Description**: In a scenario where VMM is monitored using Operations Manager, performance monitoring for VMM server fails with *Access denied*  event error. Service users don't have permission to access VirtualMachineManager-Server/Operational event log.

**Workaround**: Change the security descriptor for Operational event log registry with the following command, and then restart the event log service and health log service.

```
reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Channels\Microsoft-VirtualMachineManager-Server/Operational /v ChannelAccess /t REG_SZ /d O:BAG:SYD:(D;;0xf0007;;;AN)(D;;0xf0007;;;BG)(A;;0xf0007;;;SY)(A;;0x7;;;BA)(A;;0x3;;;NS)(A;;0x1;;;IU)(A;;0x1;;;SU)"
```
This command adds the service user to the list of allowed users, who can access VirtualMachineManager-Server/Operational event log.

## Set-SCVMSubnet -RemovePortACL job completes in VMM without removing portACL association from NC VMSubnet object

**Description**: Set-SCVMSubnet -RemovePortACL job completes in VMM without removing portACL association from NC VMSubnet object due to which Remove-PortACL job fails with NC Exception that is still in use.

**Workaround**: Remove the VMSubnet from VMM and then remove Port-ACL.

 Import-Module NetworkController

 #Replace the URI of the Network Controller with REST IP or FQDN

 ```
 $uri = "<NC FQDN or IP>"

 ```

 #Provide NC Admin credentials

 ```
 $cred = Get-Credential

 ```

 #Identify the virtual network that contains the subnet

 ```
 $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Fabrikam_VNet1" -Credential $cred

 ```

 #Identify the subnet for which the ACL needs to be removed

 ```
 $vnet.Properties.Subnets[0].Properties = $vnet.Properties.Subnets[0].Properties | Select-Object -Property * -ExcludeProperty AccessControlList

 ```

 #Update

 ```
 New-NetworkControllerVirtualNetwork -ResourceId "Fabrikam_VNet1" -ConnectionUri $uri –Properties $vnet.Properties -Credential $cred

 ```
