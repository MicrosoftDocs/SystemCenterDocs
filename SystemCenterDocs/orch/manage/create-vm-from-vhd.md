---
title: Create VM from VHD
description: The Create VM from VHD activity is used to create a new virtual machine from an existing virtual hard disk.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87146c7c-d1e7-4faf-a079-7814a81b9f1b
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create VM from VHD

Applies To: System Center 2016 - Orchestrator

The Create VM from VHD activity is used to create a new virtual machine from an existing virtual hard disk.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create VM from VHD Required Properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Disk Bus   | The IDE or SCSI bus to which to attach the virtual disk drive. If you select &lt;Auto&gt; then the first available value will be selected.   |   |
| Disk File Name   | The name of the destination VHD   |   |
| Disk Logical Unit Number (LUN) | The logical unit number (LUN) for a virtual disk drive object on an IDE or SCSI bus. If you select &lt;Auto&gt; then the first available value will be selected. |   |
| Path   | The path of the virtual machine in the format C:\\VMM   |   |
| Virtual Hard Disk Path   | The location of the VHD used to create the virtual machine   |   |
| VM Host   | The full computer name of the host computer for Virtual Machine Manager   |   |
| VM Name   | An alphanumeric name of your choice for the virtual machine   |   |

## Create VM from VHD Optional Properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| CPU Count   | The number of CPUs on the virtual machine   |   |
| CPU Type   | The type of CPU for the virtual machine   |   |
| Custom Priority  | A two-digit value of your choice to describe the priority of the virtual machine   |   |
| Delay Start (s)  | The number of seconds to wait after the virtualization service starts before automatically starting the virtual machine. This value is used to stagger the startup time of multiple virtual machines to help reduce the demand on the physical computer's resources. A typical setting could be 30 to 60 seconds.   |   |
| Description   | An alphanumeric description of your choice for the virtual machine   |   |
| Hardware Profile | The full path and file name of the library resource containing hardware specifications that can be applied to a new virtual machine or to a virtual machine Template. A hardware profile can contain specifications for CPU, memory, network adapters, a DVD drive, a floppy drive, COM ports, and the priority given to the virtual machine when allocating resources on a virtual machine host. |   |
| Memory (MB)   | The total amount of memory on the host that is assigned to the virtual machine in megabytes (MB)   |   |
| Network Location | The network location for a physical network adapter or for a virtual network adapter   |   |
| Network Spoofing | True or False   |   |
| Network Tag   | An alphanumeric value to differentiate the host's virtual networks, based on a criterion such as throughput or security. Network tags can be used to match virtual machines with suitable hosts.   |   |
| Network VLAN ID  | A numeric identifier in the range 1 through 4094 for the Network VLAN   |   |
| Operating System | The virtual machine operating system   |   |
| Owner   | The owner of the Virtual Machine Manager activity in the form of a valid domain user account   |   |
| Start Action   | The behavior of the virtual machine when the virtualization service starts. The valid values are: Never Auto Turn On, Always Auto Turn On, or Turn On VM If Running When VS Stopped.   |   |
| Stop Action   | The behavior of the virtual machine when the virtualization service stops. The valid values are: Save, Turn Off, or Shut Down Guest OS.   |   |
| Virtual Network  | The name of the Virtual Network   |   |

## Create VM from VHD Published Data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the virtual machine was added in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Backup Enabled   | True or False   |   |
| Boot Order   | The order of devices that the virtual machine on a Hyper-V host uses to start up. The valid values are: CD, IDE Hard Drive, PXE Boot, or Floppy   |   |
| Checkpoint Location   | The full path of the checkpoint for the virtual machine, in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Computer Name   | The name of the virtual machine   |   |
| Cost Center   | An alphanumeric value for the Self-Service Portal   |   |
| CPU Count   | The number of CPUs on the virtual machine   |   |
| CPU Max (%)   | A two-digit percent value that represents the upper bound for CPU usage while the virtual machine is running   |   |
| CPU Reserve (%)   | A two-digit percent value that represents the CPU resources that are set aside for the host operating system to use   |   |
| CPU Type   | The type of CPU for the virtual machine   |   |
| CPU Utilization (%)   | A two-digit percent value that represents the upper bound for CPU usage while the virtual machine is running   |   |
| Creation Source   | The name of the source that was used to create the virtual machine; for example, the name of another virtual machine, a VHD name, or Unknown   |   |
| Creation Time   | The date and time that the virtual machine was created in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Custom Priority   | A two-digit value to describe the priority of the virtual machine   |   |
| Custom Properties   | Up to 10 custom values that can be used to identify, track, and sort virtual machines. The values are published in one list.   |   |
| Data Exchange Enabled   | True or False   |   |
| Delay Start (s)   | The number of seconds to wait after the virtualization service starts before automatically starting the virtual machine.   |   |
| Description   | An alphanumeric description of the virtual machine   |   |
| Disk Bus   | The IDE or SCSI bus to which to attach the virtual disk drive   |   |
| Disk File Name   | The name of the VHD   |   |
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second \[IOPS\] that can be performed with acceptable latency   |   |
| Disk Logical Unit Number (LUN)   | The logical unit number (LUN) for a virtual disk drive object on an IDE or SCSI bus   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Expected CPU Utilization   | A two-digit percent value that represents the average CPU usage for the virtual machine   |   |
| Failed Job ID   | The unique identifier (GUID) of the most recent failed job   |   |
| Hardware Profile   | The full path and file name of the library resource containing hardware specifications that can be applied to the new virtual machine or to a virtual machine Template   |   |
| Has Pass-through Disk   | True or False   |   |
| Has VM Additions   | True or False. If True, the virtual machine has additional software installed on the Guest Operating System to assist with virtualization, also known as virtual machine Guest Services.   |   |
| Heartbeat Enabled   | True or False   |   |
| Host Group Path   | The path of the virtual machine under its host group, in the format All Hosts\\VIRTUAL MACHINE name   |   |
| Host ID   | The unique identifier (GUID) of the host computer for Virtual Machine Manager   |   |
| Host Type   | VMHost   |   |
| Is Highly Available   | True or False   |   |
| Is Tag Empty   | True or False   |   |
| Is Undergoing Live Migration   | True or False   |   |
| Job Additional Messages   | Details about the Create VM from VHD job returned by Virtual Machine Manager   |   |
| Job Status   | The status of the Create VM from VHD job returned by Virtual Machine Manager. Valid values are as follows: Failed, Completed, or Completed with Info   |   |
| Last Restored VM Checkpoint   | The name of the most recently restored Checkpoint   |   |
| Library Group   | The name of the library group   |   |
| Library Server   | The name of the library server   |   |
| Limit CPU Functionality   | True or False. Virtual Machine Manager uses this setting to determine whether the CPU should be put into a compatibility mode for virtual machine running Windows NT.   |   |
| Location   | The virtual machine location in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Marked As Template   | True or False   |   |
| Memory (MB)   | The total amount of memory on the host that is assigned to the virtual machine in MB   |   |
| Modified Time   | The date and time that the virtual machine was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent Task   | The name of the most recent task for the virtual machine, for example, Start virtual machine   |   |
| Network Location   | The network location for a physical network adapter or for a virtual network adapter   |   |
| Network Spoofing   | True or False   |   |
| Network Tag   | An alphanumeric value to differentiate the host's virtual networks, based on a criterion such as throughput or security. Network tags can be used to match virtual machines with suitable hosts. |   |
| Network Spoofing   | True or False   |   |
| Network Utilization   | A two-digit network utilization value   |   |
| Network VLAN ID   | A numeric identifier in the range 1 through 4094 for the Network VLAN   |   |
| NumLock Enabled   | True or False   |   |
| Operating System   | The type of operating system for the virtual machine   |   |
| Operating System Shutdown Enabled   | True or False   |   |
| Owner   | The virtual machine owner, in the format Domain\\User   |   |
| Owner SID   | The unique identifier of the owner of the virtual machine in the format S-1-5-21-GUID   |   |
| Pass-through Disk   | A list of names of pass-through disks   |   |
| Path   | The path of the virtual machine in the format C:\\VMM   |   |
| Quota Point   | A three-digit number that represents a unit by which the virtual machine quota for self-service users is calculated   |   |
| Self Service User Role   | The User Role that allows users to create virtual machines using templates   |   |
| Share SCSI Bus   | True or False   |   |
| Source Object Type   | The type of the source object that was used to create the virtual machine; for example, virtual machine, Template, or VHD.   |   |
| Source Template Name   | The name of the virtual machine Template that was used to create the virtual machine   |   |
| Start Action   | The behavior of the virtual machine when the virtualization service starts. The valid values are: Never Auto Turn On, Always Auto Turn On, or Turn On VM If Running When VS Stopped.   |   |
| Status   | The status of the virtual machine. Valid values are: Running, Paused, PowerOff, or Missing   |   |
| Stop Action   | The behavior of the virtual machine when the virtualization service stops. The valid values are: Save, Turn Off, or Shut Down Guest OS.   |   |
| Tag   | An alphanumeric value used to locate related virtual machines   |   |
| Tiered Perf Data   | The unique identifier (GUID) of the ordered performance data   |   |
| Time Synchronization Enabled   | True or False   |   |
| Total Size   | The total size of the virtual machine, including all disks and configuration files   |   |
| Undo Disks Enabled   | True or False. If True, the virtual machine can undo any changes when shutting down.   |   |
| Unsupported Reason   | If an error occurs during creation of the virtual machine, this message text describes the reason that the attempted action is not supported   |   |
| Use Hardware Assisted Virtualization | True or False   |   |
| User Role ID   | The unique identifier (GUID) of the user role that allows users to create virtual machines   |   |
| Virtual COM Ports   | A list of the names of the Virtual COM Ports. Always COM1 or COM2.   |   |
| Virtual DVD Drives   | A list of the names of Virtual DVD Drives   |   |
| Virtual Disk Drives   | A list of the names of Virtual Disk Drives   |   |
| Virtual Floppy Drive   | A list of the names of Virtual Floppy Drives   |   |
| Virtual Hard Disk Path   | The location of the VHD used to create the virtual machine   |   |
| Virtual Hard Disks   | A list of the names of VHDs   |   |
| Virtualization Platform   | The virtualization platform. Valid values are: HyperV, VMWareESX, or Unknown   |   |
| Virtual Network   | The name of the virtual network   |   |
| Virtual Network Adapters   | A list of the names of Virtual Network Adapters   |   |
| Virtual SCSI Adapters   | A list of the names of Virtual SCSI Adapters   |   |
| VMC Path   | The virtual machine configuration file path, in the format C:\\VMM\\DRDemo-DataTier\\VirtualMachines\\abc12345-d6ef-78g9-h0ij-1kl2-34m56n7890p12.xml   |   |
| VM Host   | The full computer name of the host computer for Virtual Machine Manager   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine   |   |
| VM Name   | The name of the virtual machine   |   |
| VM Platform ID   | The unique identifier (GUID) of the virtual machine inside the platform, for example, Hyper-V, VMware, or Virtual Server   |   |
