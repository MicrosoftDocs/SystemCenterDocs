---
title: Create VM from Template
description: The Create VM from Template activity is used to create a new virtual machine from the specified template.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c5d8bf4-cb22-443f-b5fb-ff4361e081a6
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Create VM from Template
=======================

Applies To: System Center 2016 - Orchestrator

The Create VM from Template activity is used to create a new virtual machine from the specified template.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Create VM from Template Required Properties
-------------------------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Destination Type   | Specify the type of VM to create   |   |
| Destination   | Description of destination   |   |
| Path   | The path of the virtual machine in the format C:\\VMM   |   |
| Source Template Name   | The name of the virtual machine Template used to create the virtual machine |   |
| Cloud Capability Profile | Specify the Cloud Apability object defined in the VMM 2016 library.   |   |
| VM Name   | An alphanumeric name of your choice for the virtual machine   |   |

Create VM from Template Optional Properties
-------------------------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Admin Password   | The password for the Local Administrator account   |   |
| Admin User Name   | The account name for the Local Administrator account   |   |
| Answer File Path   | The full path and file name of the script object stored in the Virtual Machine Manager library to be used as an answer file. The answer file contains the product key, the credentials with permissions to join a domain, and the computer name wildcard character (\*). These allow the computer name to be randomly generated.   |   |
| CPU Count   | The number of CPUs on the virtual machine   |   |
| CPU Type   | The type of CPU for the virtual machine   |   |
| Delay Start (s)   | The number of seconds to wait after the virtualization service starts before automatically starting the virtual machine. This value is used to stagger the startup time of multiple virtual machines to help reduce the demand on the physical computer's resources. A typical setting could be 30 to 60 seconds.   |   |
| Description   | An alphanumeric description of your choice for the virtual machine   |   |
| Destination Computer Name | The name of the new virtual machine   |   |
| Domain Name   | The name of the domain to join   |   |
| Domain Password   | The password used to join the computer to a domain, if Domain Namehas a value   |   |
| Domain User Name   | The user name used to join the computer to a domain, if Join Domain = True   |   |
| Full Name   | The full name of the owner that is specified during Sysprep as part of operating system install   |   |
| Guest OS Profile   | The full path and file name of the library resource that contains the most common settings from a Sysprep.inf file. This includes the computer name and domain or workgroup settings, which can be applied to a virtual machine Template   |   |
| Hardware Profile   | The full path and file name of the library resource containing hardware specifications that can be applied to a new virtual machine or to a virtual machine Template. A hardware profile can contain specifications for CPU, memory, network adapters, a DVD drive, a floppy drive, COM ports, and the priority given to the virtual machine when allocating resources on a virtual machine host. |   |
| Memory (MB)   | The total amount of memory on the host that is assigned to the virtual machine in megabytes (MB)   |   |
| Network Location   | The network location for a physical network adapter or for a virtual network adapter   |   |
| Network Spoofing   | True or False   |   |
| Network Tag   | An alphanumeric value of your choice used to locate related networks   |   |
| Network VLAN ID   | A numeric identifier in the range 1 through 4094 for the Network VLAN   |   |
| Operating System   | The virtual machine operating system   |   |
| Organization Name   | The name of the organization of the person in whose name the virtual machine is registered   |   |
| Owner   | The owner of the Virtual Machine Manager object in the form of a valid domain user account   |   |
| Product Key   | Windows product key   |   |
| Start Action   | The behavior of the virtual machine when the virtualization service starts. The valid values are as follows: Never Auto Turn On, Always Auto Turn On, or Turn On VM If Running When VS Stopped.   |   |
| Stop Action   | The behavior of the virtual machine when the virtualization service stops. The valid values are: Save, Turn Off, or Shut Down Guest OS.   |   |
| Time Zone   | The time zone of the virtual machine   |   |
| Virtual Network   | The name of the virtual network   |   |
| Logical Network   | The name or IP subnet for the logical network.   |   |
| Workgroup Name   | The name of the workgroup to join   |   |

Create VM from Template Published Data
--------------------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the virtual machine was added in the formatyyyy-mm-dd hh:mm:ss AM or PM   |   |
| Admin Password   | The password for the Local Administrator account   |   |
| Admin User Name   | The account name for the Local Administrator account   |   |
| Answer File Path   | The full path and file name of the script object stored in the Virtual Machine Manager library to be used as an answer file. The answer file contains the product key, the credentials with permissions to join a domain, and the computer name wildcard character (\*). These allow the computer name to be randomly generated.   |   |
| Backup Enabled   | True or False   |   |
| Boot Order   | The order of devices that the virtual machine on a Hyper-V host uses to start up. The value values are: CD, IDE Hard Drive, PXE Boot, or Floppy   |   |
| Checkpoint Location   | The full path of the checkpoint for the virtual machine, in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Computer Name   | The name of the virtual machine   |   |
| Cost Center   | An alphanumeric value for the Self-Service Portal   |   |
| CPU Count   | The number of CPUs on the virtual machine   |   |
| CPU Max (%)   | Two-digit percent value that represents the upper bound for CPU usage while the virtual machine is running   |   |
| CPU Reserve (%)   | Two-digit percent value of CPU resources that are set aside for the host operating system to use   |   |
| CPU Type   | The type of CPU for the virtual machine   |   |
| CPU Utilization (%)   | Two-digit percent value that represents the CPU utilization threshold that will trigger a monitor for the virtual machine   |   |
| Creation Source   | The name of the source that was used to create the virtual machine, for example, the name of another virtual machine, a VHD name, or Unknown   |   |
| Creation Time   | The date and time that the virtual machine was created in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Custom Properties   | Up to 10 custom values that can be used to identify, track, and sort virtual machines. The values are published in one list.   |   |
| Data Exchange Enabled   | True or False   |   |
| Delay Start (s)   | The number of seconds to wait after the virtualization service starts before automatically starting the virtual machine   |   |
| Destination Computer Name   | The name of the new virtual machine   |   |
| Domain Name   | The name of the domain joined   |   |
| Domain Password   | The password used to join the computer to a domain, if Domain Name has a value   |   |
| Domain User Name   | The user name used to join the computer to a domain, if Join Domain = True   |   |
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second \[IOPS\] that can be performed with acceptable latency   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Expected CPU Utilization %   | Two-digit percent value that represents the average CPU usage for the virtual machine   |   |
| Failed Job ID   | The unique identifier (GUID) of the most recent failed job   |   |
| Full Name   | The full name of the owner that is specified during Sysprep as part of operating system install   |   |
| Guest OS Profile   | The full path and file name of the library resource containing the most common settings from a Sysprep.inf file, including the computer name and domain or workgroup settings, that was used to create the virtual machine   |   |
| Hardware Profile   | The full path and file name of the library resource containing hardware specifications that can be applied to a new virtual machine or to a virtual machine Template. A hardware profile can contain specifications for CPU, memory, network adapters, a DVD drive, a floppy drive, COM ports, and the priority given to the virtual machine when allocating resources on a virtual machine host. |   |
| Has Pass-through Disk   | True or False   |   |
| Has VM Additions   | True or False. If True, the virtual machine has additional software installed on the Guest Operating System to assist with virtualization, also known as virtual machine Guest Services.   |   |
| Heartbeat Enabled   | True or False   |   |
| Host Group Path   | The path of the virtual machine under its host group, in the format All Hosts\\virtual machineame   |   |
| Host ID   | The unique identifier (GUID) of the host computer   |   |
| Host Type   | VMHost   |   |
| Highly Available   | True or False   |   |
| Is Tag Empty   | True or False   |   |
| Is Undergoing Live Migration   | True or False   |   |
| Job Additional Messages   | Details about the Create VM from Template job returned by Virtual Machine Manager   |   |
| Job Status   | The status of the Create VM from Template job returned by Virtual Machine Manager. Valid values are: Failed, Completed, or Completed With Info.   |   |
| Last Restored VM Checkpoint   | The name of the most recently restored virtual machine Checkpoint   |   |
| Library Group   | The name of the library group   |   |
| Library Server   | The name of the library server   |   |
| Limit CPU Functionality   | True or False. Virtual Machine Manager uses this setting to determine whether the CPU should be put into a compatibility mode for virtual machines running Windows NT.   |   |
| Location   | The virtual machine location in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Marked As Template   | True or False   |   |
| Memory (MB)   | The total amount of memory on the host that is assigned to the virtual machine in MB   |   |
| Modified Time   | The date and time that the virtual machine was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent Task   | The name of the most recent task for the virtual machine, for example, Start virtual machine   |   |
| Network Location   | The network location for a physical network adapter or for a virtual network adapter   |   |
| Network Spoofing   | True or False   |   |
| Network Tag   | An alphanumeric value used to locate related networks   |   |
| Network Utilization   | A two-digit network utilization value   |   |
| Network VLAN ID   | A numeric identifier in the range 1 through 4094 for the Network VLAN   |   |
| NumLock Enabled   | True or False   |   |
| Organization Name   | The name of the organization of the person in whose name the virtual machine is registered   |   |
| Operating System   | The type of operating system for the virtual machine   |   |
| Operating System Shutdown Enabled   | True or False   |   |
| Owner   | The virtual machine owner, in the format Domain\\User   |   |
| Owner SID   | The unique identifier of the owner of the virtual machine in the format S-1-5-21-GUID   |   |
| Pass-through Disks   | A list of names of pass-through disks   |   |
| Path   | The path of the virtual machine in the format C:\\VMM   |   |
| Product Key   | The Windows product key   |   |
| Quota Point   | A three digit number for the virtual machine that represents a unit by which the virtual machine quota for self-service users is calculated   |   |
| Self Service User Role   | The user role that allows users to create virtual machines using templates   |   |
| Share SCSI Bus   | True or False   |   |
| Source Object Type   | The type of the source object that was used to create the virtual machine; for example, virtual machine, Template, or VHD   |   |
| Source Template Name   | The name of the virtual machine Template used to create the virtual machine   |   |
| Start Action   | The behavior of the virtual machine when the virtualization service starts. The valid values are: Never Auto Turn On, Always Auto Turn On, or Turn On VM If Running When VS Stopped.   |   |
| Status   | The status of the virtual machine. Valid values are: Running, Paused, Power Off, or Missing   |   |
| Stop Action   | The behavior of the virtual machine when the virtualization service stops. The valid values are: Save, Turn Off, or Shut Down Guest OS.   |   |
| Tag   | An alphanumeric value used to locate related virtual machines   |   |
| Tiered Perf Data   | The unique identifier (GUID) of the ordered performance data   |   |
| Time Zone   | The time zone selected when the virtual machine was created   |   |
| Time Synchronization Enabled   | True or False   |   |
| Total Size   | The total size of the virtual machine, including all disks and configuration files   |   |
| Undo Disks Enabled   | True or False. If True, the virtual machine can undo any changes when shutting down.   |   |
| Unsupported Reason   | If an error occurs during creation of the virtual machine, this message text describes the reason that the attempted action is not supported   |   |
| Use Hardware Assisted Virtualization | True or False   |   |
| User Role   | The user role that allows users to create virtual machines   |   |
| User Role ID   | The unique identifier (GUID) of the user role that allows users to create virtual machines   |   |
| Virtual COM Ports   | A list of the names of the Virtual COM Ports. Always COM1 or COM2.   |   |
| Virtual DVD Drives   | A list of the names of Virtual DVD Drives   |   |
| Virtual Disk Drives   | A list of the names of Virtual Disk Drives   |   |
| Virtual Floppy Drive   | A list of the names of Virtual Floppy Drives   |   |
| Virtual Hard Disks   | A list of the names of Virtual Hard Disks   |   |
| Virtualization Platform   | The virtualization platform. Valid values are: HyperV, VMWareESX, or Unknown.   |   |
| Virtual Network   | The name of the virtual network   |   |
| Virtual Network Adapters   | A list of the names of Virtual Network Adapters   |   |
| Virtual SCSI Adapters   | A list of the names of Virtual SCSI Adapters   |   |
| VMC Path   | The virtual machine Configuration file path, in the format C:\\VMM\\DRDemo-DataTier\\VirtualMachines\\abc12345-d6ef-78g9-h0ij-1kl2-34m56n7890p12.xml   |   |
| VM Host   | The full computer name of the host computer for Virtual Machine Manager   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine   |   |
| VM Name   | The name of the virtual machine   |   |
| VM Platform ID   | The unique identifier (GUID) of the virtual machine inside the platform, for example, Hyper-V, VMware, or Virtual Server   |   |
| Workgroup Name   | The name of the workgroup joined   |   |
