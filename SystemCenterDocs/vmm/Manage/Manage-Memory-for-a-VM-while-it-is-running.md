---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Manage Memory for a VM while it is running
ms.technology:  virtual-machine-manager
ms.assetid:  bb68bc2f-cd43-4c40-969a-fa2cbbdc6fef
---

# Manage Memory for a VM while it is running

>Applies To: 

With System Center 2016 Virtual Machine Manager, you can now modify the memory configuration of a running virtual machine(VM) that uses static memory. This feature helps in eliminating workload downtime due to reconfiguration. You can increase or decrease the memory allocation, or switch the virtual machine to dynamic memory. Note that users can already modify dynamic memory for a running VM from VMM and this feature is about modifying the static memory.

Note: This functionality is enabled through PowerShell only and is not exposed through the VMM Console. This enhancement applies to virtual machines running Windows Server Technical Preview on host computers running Windows Server Technical Preview. 

### **Sample Cmdlets**
**Example 1**: Change the static memory for a running virtual machine
The first command gets the virtual machine object named VM01, and then stores the object in the $VM variable. The second command changes the memory allocated to VM01 to 1024 MB.
```
PS C:\> $VM = Get-SCVirtualMachine -Name "VM01"
PS C:\> Set-SCVirtualMachine -VM $VM -MemoryMB 1024
```
**Example 2:** Enable Dynamic Memory for a running virtual machine
The first command gets the virtual machine object named VM02, and then stores the object in the $VM variable. The second command enables Dynamic Memory, sets the startup memory to 1024 MB, and the maximum memory to 2048 MB
```
PS C:\> $VM = Get-SCVirtualMachine -Name "VM02"
PS C:\> Set-SCVirtualMachine -VM $VM -DynamicMemoryEnabled $True -MemoryMB 1024 -DynamicMemoryMaximumMB 2048
```


