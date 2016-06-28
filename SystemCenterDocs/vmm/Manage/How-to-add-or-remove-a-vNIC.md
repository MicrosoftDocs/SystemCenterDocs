---
title: How to add or remove a vNIC
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0e34a1c-5fd8-425f-a028-194f658b6ebb
---
# How to add or remove a vNIC

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can now add and remove virtual network adapters from running virtual machines(VMs). This feature helps in eliminating workload downtime due to reconfiguration.

Note: This functionality is enabled through PowerShell only and is not exposed through the VMM Console. This enhancement applies to Generation 2 virtual machines running on Windows Server Technical Preview hosts. 

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


