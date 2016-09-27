---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to add or remove a vNIC
ms.technology:  virtual-machine-manager
ms.assetid:  d0e34a1c-5fd8-425f-a028-194f658b6ebb
---

# How to add or remove a vNIC

>Applies To: System Center 2016  - Virtual Machine Manager

You can now add and remove virtual network adapters from running virtual machines(VMs). This feature helps in eliminating workload downtime due to reconfiguration.

Note: This enhancement applies to only Generation 2 virtual machines running on Windows Server Technical Preview hosts.

This functionality is enabled both through PowerShell and the VMM Administrator Console. Below are few sample PowerShell cmdlets on how to add/remove a new virtual network adapter to a running VM:

### **Sample Cmdlets**
**Example 1:** The following PowerShell command will add a virtual network adapter (vNIC) to a running VM.
The first command gets the virtual machine object named VM01, and then stores the object in the $VM variable.The second command creates a virtual network adapter on VM01.
```
PS C:\> $VM = Get-SCVirtualMachine -Name "VM01"
PS C:\> New-SCVirtualNetworkAdapter -VM $VM -Synthetic
```
**Example 2:**The following PowerShell commands will remove a vNIC from a running VM.
The first command gets the virtual machine object named VM02, and then stores the object in the $VM variable. The second command gets the virtual network adapter object on VM02, and then stores the object in the $Adapter variable. The last command removes the virtual network adapter object stored in $Adapter from VM02.

```
PS C:\> $VM = Get-SCVirtualMachine -Name "VM02"
PS C:\> $Adapter = Get-SCVirtualNetworkAdapter -VM $VM
PS C:\> Remove-SCVirtualNetworkAdapter -VirtualNetworkAdapter $Adapter
```
**Note:** The second PowerShell sample above assumes that there is only one vNIC on the virtual machine.

For more details on how to add/remove a virtual network adapter from the VMM Administrator Console, see [How to Add and Configure Network Adapters for a Virtual Machine](https://technet.microsoft.com/en-in/library/bb740792.aspx)
