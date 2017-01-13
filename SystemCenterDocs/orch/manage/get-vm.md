---
title: Get VM
description: The Get VM activity is used to retrieve an existing VM based on the filters you specify.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7f27148-70cc-498d-b134-8b7e8c4a4ca9
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get VM

Applies To: System Center 2016 - Orchestrator

The Get VM activity is used to retrieve an existing VM based on the filters you specify.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get VM Filters


| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | Select a date from the calendar. Use the up and down arrows to select a time.   |   |
| Backup Enabled   | True or False   |   |
| Boot Order   | The order of devices that the virtual machine on a Hyper-V host uses to start up. The valid values are: CD, IDE Hard Drive, PXE Boot, or Floppy   |   |
| Computer Name   | The name of the virtual machine   |   |
| Cost Center   | An alphanumeric value for the Self-Service Portal   |   |
| CPU Count   | The number of CPUs on the virtual machine   |   |
| CPU Max (%)   | A two-digit percent value that represents the upper bound for CPU usage while the virtual machine is running   |   |
| CPU Reserve (%)   | A two-digit percent value of CPU resources that are set aside for the host operating system to use   |   |
| CPU Type   | The type of CPU for the virtual machine   |   |
| CPU Utilization (%)   | A two-digit percent value that represents the CPU utilization threshold that will trigger a monitor for the virtual machine   |   |
| Creation Source   | The name of the source that was used to create the virtual machine; for example, the name of another virtual machine, a VHD name, or Unknown   |   |
| Creation Time   | The date and time that the virtual machine was created in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Custom Priority   | A two-digit value to describe the priority of the virtual machine   |   |
| Custom Property 1   | The value of Custom Property 1   |   |
| Custom Property 2   | The value of Custom Property 2   |   |
| Custom Property 3   | The value of Custom Property 3   |   |
| Custom Property 4   | The value of Custom Property 4   |   |
| Custom Property 5   | The value of Custom Property 5   |   |
| Custom Property 6   | The value of Custom Property 6   |   |
| Custom Property 7   | The value of Custom Property 7   |   |
| Custom Property 8   | The value of Custom Property 8   |   |
| Custom Property 9   | The value of Custom Property 9   |   |
| Custom Property 10   | The value of Custom Property 10   |   |
| Data Exchange Enabled   | True or False   |   |
| Delay Start (s)   | The number of seconds to wait after the virtualization service starts before automatically starting the virtual machine   |   |
| Deployment State   | Valid values are Deployed, Deploying, DeploymentFailed, Servicing, ServicingFailed. Stored, and Undeployed   |   |
| Description   | An alphanumeric description of your choice for the virtual machine   |   |
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second \[IOPS\] that can be performed with acceptable latency.   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Expected CPU Utilization   | A two-digit percent value that represents the average CPU usage for the virtual machine   |   |
| Failed Job ID   | The unique identifier (GUID) of the most recent failed job   |   |
| Has Pass-through Disk   | True or False   |   |
| Has VM Additions   | True or False   |   |
| Heartbeat Enabled   | True or False   |   |
| Host Group Path   | The path of the virtual machine under its host group, in the format All Hosts\\virtual machine name.   |   |
| Host ID   | The unique identifier (GUID) for the host computer   |   |
| Host Name   | The name of the host computer   |   |
| Host Type   | virtual machine host or library server   |   |
| Is Highly Available   | True or False   |   |
| Is Tag Empty   | True or False   |   |
| Is Undergoing Live Migration   | True or False   |   |
| Library Group   | The name of the library group   |   |
| Library Server   | The name of the library server   |   |
| Limit CPU Functionality   | True or False. Virtual Machine Manager uses this setting to determine whether the CPU should be put into a compatibility mode for virtual machines running Windows NT.   |   |
| Location   | The virtual machine location in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Marked as a Template   | True or False   |   |
| Memory (MB)   | The total amount of memory on the host that is assigned to the virtual machine in megabytes (MB)   |   |
| Modified Time   | The date and time that the virtual machine was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Network Utilization   | A two-digit network utilization value   |   |
| Numlock Enabled   | True or False   |   |
| Operating System   | The type of operating system for the virtual machine   |   |
| Operating System Shutdown Enabled | True or False   |   |
| Owner   | The virtual machine owner, in the format Domain\\User   |   |
| Owner SID   | The unique identifier of the owner of the virtual machine, in the format S-1-5-21-GUID   |   |
| Quota Point   | A three digit number for the virtual machine that represents a unit by which the virtual machine quota for self-service users is calculated. Quota points are assigned to the templates that self-service users use to create their virtual machines.   |   |
| Share SCSI Bus   | True or False   |   |
| Start Action   | The behavior of the virtual machine when the virtualization service starts. The valid values are: Never Auto Turn On, Always Auto Turn On, or Turn On VM If Running When VS Stopped.   |   |
| Status   | The status of the virtual machine. Valid values are: Running, Power Off, Powering Off, Saved, Saving, Restoring, Paused, Discard Saved State, Starting, Merging Drives, Deleting, Discarding Drives, Pausing, Under Creation, Creation Failed, Stored, Under Template Creation, Template Creation Failed, Customization Failed, Under Update, Update Failed, Under Migration, Migration Failed, Creating Checkpoint, Deleting Checkpoint, Recovering Checkpoint, Checkpoint Failed, Initializing Checkpoint Operation, Finishing Checkpoint Operation, Missing, Host Not Responding, Unsupported, Incomplete VM Config, Unsupported Shared Files, Unsupported Cluster, P2V Creation Failed, or V2V Creation Failed. |   |
| Stop Action   | The behavior of the virtual machine when the virtualization service stops. The valid values are: Save, Turn Off, or Shut Down Guest OS.   |   |
| Tag   | An alphanumeric value used to locate related virtual machines   |   |
| Time Synchronization Enabled   | True or False   |   |
| Total Size   | The total size of the virtual machine, including all disks and configuration files   |   |
| Undo Disks Enabled   | True or False   |   |
| User Role   | The user role that allows users to create virtual machines.   |   |
| Virtual Disk Drives   | A list of the names of Virtual Disk Drives   |   |
| Virtual DVD Drives   | A list of the names of Virtual DVD Drives   |   |
| Virtual Hard Disks   | A list of the names of Virtual Hard Disks   |   |
| Virtualization Platform   | The virtualization platform. Valid values are: HyperV, VMWareESX, or Unknown.   |   |
| Virtual Network Adapters   | A list of the names of Virtual Network Adapters   |   |
| Virtual SCSI Adapters   | A list of the names of Virtual SCSI Adapters   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine   |   |
| VM Name   | The name of the virtual machine   |   |
| VM Platform ID   | The unique identifier (GUID) of the virtual machine inside the platform, for example, Hyper-V, VMware, or Virtual Server   |   |

## Get VM Published Data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the virtual machine was added in the yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Backup Enabled   | True or False   |   |
| Boot Order   | The order of devices that the virtual machine on a Hyper-V host uses to start up. The valid values are: CD, IDE Hard Drive, PXE Boot, or Floppy   |   |
| Checkpoint Location   | The full path of the checkpoint for the virtual machine, in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Cloud   | A collection of resources that are provisioned and managed on-premise by an organization   |   |
| Cloud Capability Profile   | The configurable options that define your cloud   |   |
| Compliance Status   | True or False   |   |
| Computer Name   | The name of the virtual machine   |   |
| Computer Tier   | Defined by a VM template and a Load Balancer template   |   |
| Cost Center   | An alphanumeric value for the Self-Service Portal   |   |
| CPU Count   | The number of CPUs on the virtual machine   |   |
| CPU Max (%)   | A two-digit percent value that represents the upper bound for CPU usage while the virtual machine is running   |   |
| CPU Reserve (%)   | A two-digit percent value of CPU resources that are set aside for the host operating system to use   |   |
| CPU Type   | The type of CPU for the virtual machine   |   |
| CPU Utilization (%)   | A two-digit percent value that represents the CPU utilization threshold that will trigger a monitor for the virtual machine   |   |
| Creation Source   | The name of the source that was used to create the virtual machine; for example, the name of another virtual machine, a VHD name, or Unknown   |   |
| Creation Time   | The date and time that the virtual machine was created in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Custom Priority   | A two-digit value to describe the priority of the virtual machine   |   |
| Custom Properties   | Up to 10 custom values that can be used to identify, track, and sort virtual machines. The values are published in one list.   |   |
| Data Exchange Enabled   | True or False   |   |
| Delay Start (s)   | The number of seconds to wait after the virtualization service starts before automatically starting the virtual machine   |   |
| Deployment State   | Valid values are Deployed, Deploying, DeploymentFailed, Servicing, ServicingFailed. Stored, and Undeployed   |   |
| Description   | An alphanumeric description of the virtual machine   |   |
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second \[IOPS\] that can be performed with acceptable latency.   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Expected CPU Utilization   | A two-digit percent value that represents the average CPU usage for the virtual machine   |   |
| Failed Job ID   | The unique identifier (GUID) of the most recent failed job   |   |
| Has Pass-through Disk   | True or False   |   |
| Has Saved State   | True or False   |   |
| Has VM Additions   | True or False. If True, the virtual machine has additional software installed on the Guest Operating System to assist with virtualization, also known as VM Guest Services.   |   |
| Heartbeat Enabled   | True or False   |   |
| Host Group Path   | The path of the virtual machine under its host group, in the format All Hosts\\virtual machine name.   |   |
| Host ID   | The unique identifier (GUID) of the host computer   |   |
| Host Name   | The name of the host computer   |   |
| Host Type   | VMHost   |   |
| Is Highly Available   | True or False   |   |
| Is Tag Empty   | True or False   |   |
| Is Undergoing Live Migration   | True or False   |   |
| Last Restored VM Checkpoint   | The name of the most recently restored virtual machine Checkpoint   |   |
| Library Group   | The name of the library group   |   |
| Library Server   | The name of the library server   |   |
| Limit CPU Functionality   | True or False. Virtual Machine Manager uses this setting to determine whether the CPU should be put into a compatibility mode for virtual machines running Windows NT.   |   |
| Location   | The virtual machine location in the format C:\\ProgramData\\Microsoft\\Windows\\Hyper-V   |   |
| Marked As Template   | True or False   |   |
| Memory (MB)   | The total amount of memory on the host that is assigned to the virtual machine in MB   |   |
| Memory Available (%)   | The amount of memory on the host that is available to the virtual machine, in MB   |   |
| Modified Time   | The date and time that the virtual machine was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent Task   | The name of the most recent task for the virtual machine, for example, Start VM   |   |
| Network Ethernet (MAC) Address   | Static or Dynamic   |   |
| Network Location   | Select the network location   |   |
| Network Spoofing   | True or False   |   |
| Network Tag   | An alphanumeric value to differentiate the host's virtual networks, based on a criterion such as throughput or security. Network tags can be used to match virtual machines with suitable hosts. |   |
| Network Utilization   | A two-digit network utilization value   |   |
| Network VLAN ID   | The unique identifier (GUID) for the Network VLAN   |   |
| NumLock Enabled   | True or False   |   |
| Operating System   | The type of operating system for the virtual machine   |   |
| Operating System Shutdown Enabled   | True or False   |   |
| Owner   | The virtual machine owner, in the format Domain\\User   |   |
| Owner SID   | The unique identifier of the owner of the virtual machine in the format S-1-5-21-GUID   |   |
| Pass-through Disk   | A list of names of pass-through disks   |   |
| Quota Point   | A three digit number for the virtual machine that represents a unit by which the virtual machine quota for self-service users is calculated   |   |
| Self Service User Role   | The User Role that allows users to create virtual machines using templates   |   |
| Share SCSI Bus   | True or False   |   |
| Source Object Type   | The type of the source object that was used to create the virtual machine; for example, virtual machine, Template, or VHD.   |   |
| Start Action   | The behavior of the virtual machine when the virtualization service starts. The valid values are: Never Auto Turn On, Always Auto Turn On, or Turn On VM If Running When VS Stopped.   |   |
| Status   | The status of the virtual machine   |   |
| Stop Action   | The behavior of the virtual machine when the virtualization service stops. The valid values are: Save, Turn Off, or Shut Down Guest OS.   |   |
| Tag   | An alphanumeric value used to locate related virtual machines   |   |
| Tiered Perf Data   | The unique identifier (GUID) of the ordered performance data   |   |
| Time Synchronization Enabled   | True or False   |   |
| Total Size   | The total size of the virtual machine, including all disks and configuration files   |   |
| Undo Disks Enabled   | True or False. If True, the virtual machine can undo any changes when shutting down.   |   |
| Unsupported Reason   | If an error occurs during cloning, this message text describes the reason that the attempted action is not supported   |   |
| Use Hardware Assisted Virtualization | True or False   |   |
| User Role   | The user role used to get the virtual machine.   |   |
| User Role ID   | The unique identifier (GUID) of the user role that allows users to create virtual machines   |   |
| Virtual COM Ports   | A list of the names of the Virtual COM Ports. Always COM1 or COM2.   |   |
| Virtual DVD Drives   | A list of the names of Virtual DVD Drives   |   |
| Virtual Disk Drives   | A list of the names of Virtual Disk Drives   |   |
| Virtual Floppy Drives   | A list of the names of Virtual Floppy Drives   |   |
| Virtual Hard Disks   | A list of the names of Virtual Hard Disks   |   |
| Virtualization Platform   | The virtualization platform. Valid values are: HyperV, VMWareESX, or Unknown.   |   |
| Virtual Network Adapters   | A list of the names of Virtual Network Adapters   |   |
| Virtual SCSI Adapters   | A list of the names of Virtual SCSI Adapters   |   |
| VMC Path   | The virtual machine configuration file path, in the format C:\\VMM\\DRDemo-DataTier\\VirtualMachines\\abc12345-d6ef-78g9-h0ij-1kl2-34m56n7890p12.xml   |   |
| VM Host   | The full computer name of the Host computer for Virtual Machine M   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine   |   |
| VM Name   | The name of the virtual machine   |   |
| VM Platform ID   | The unique identifier (GUID) of the virtual machine inside the platform, for example, Hyper-V, virtual machineware, or Virtual Server   |   |
