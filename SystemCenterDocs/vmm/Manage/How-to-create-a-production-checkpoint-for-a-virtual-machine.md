---
title: How to create a production checkpoint for a virtual machine
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2722cbea-1c98-4574-913a-d09d87bc8ece
---
# How to create a production checkpoint for a virtual machine
Production checkpoints allow you to easily create “point in time” images of a virtual machine which can then be restored later. This is achieved by using backup technology inside the guest to create the checkpoint instead of using saved state technology. On a virtual machine running a Windows operating system production checkpoints are created with the Volume Snapshot Service (VSS). Linux virtual machines flush their file system buffers to create a file system consistent checkpoint. If you want to create checkpoints using saved state technology you can still choose to use standard checkpoints for your virtual machine. 
## Production Checkpoints in Hyper-V 
You can set one of the following four types of checkpoints for a virtual machine hosted by Hyper-V Server Role in Windows Server 2016:
1. **Disabled:** when the checkpoint for the VM is disabled no checkpoint will be taken.

2. **Production:** Production checkpoints are application consistent snapshots of a virtual machine. Hyper-V leverages the guest VSS provider to create an image of the virtual machine where all of its applications are in a consistent state. The production snapshot does not support the auto-recovery phase during creation. Applying a production checkpoint requires the restored virtual machine to boot from an off-line state just like with a restored backup. This is always more suitable for production environments. 

3. **ProductionOnly:** This option is the same as Production with one key difference: With ProductionOnly, if a production checkpoint fails then no checkpoint will be taken. This is different from Production where if a production checkpoint fails, a standard checkpoint will be taken instead.
 
4. **Standard** With a Standard checkpoint, all of the memory state of running applications gets stored so that when you apply the checkpoint the application reverts to the previous state. For many applications this would not be suitable for a production environment. Therefore this type of checkpoint is typically more suitable for development and test environments for some applications.

You can set the checkpoint with the following PowerShell command:

  Set-SCVirtualMachine –CheckpointType (Disabled, Production, ProductionOnly, Standard)
  
  The following screenshot fom the VMM Console illustrates the fields to set for creating a Production Checkpoint
  ![VMM Production Checkpoint ScreenImage/VMM-Production-Checkpoint-Screen.png)

