---
title: Create VM Activity
description: The Create VM activity is added to a runbook to create a new virtual machine.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: a7102bb9-bc30-4a8b-9ec5-73452cb9a29d
author: jyothisuri
ms.author: jsuri
robots: noindex
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Create VM Activity

The Create VM activity is added to a runbook to create a new virtual machine. The runbook can be used to create virtual machines on demand based on self-service provisioning processes.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Create VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Datastore Path   | The name of the data store used by the virtual machine.   | String   | Yes   |
| Folder Path   | The path to the folder containing the virtual machine.   | String   | Yes   |
| Guest Operating System  | The name of the guest operating system installed on this virtual machine.   | String   | Yes   |
| Host System Path   | The path to the host system of the virtual machine.   | String   | Yes   |
| Memory (MB)   | The amount of memory, in megabytes, assigned to the virtual machine.   | Integer   | No   |
| Nic (1-4)   | The name of the virtual network. You must enter a value for Nic1, but can leave Nics 2-4 blank if there are no additional networks. | String   | No   |
| Number Processors   | The number of processors assigned to the virtual machine.   | Integer   | No   |
| Power on after creation | Indicates whether to turn on the virtual machine after it's created.   | Boolean   | Yes   |
| Resource Pool Path   | The path to the resource pool used by the virtual machine.   | String   | Yes   |
| Virtual Disk Size(GB)   | The size of the virtual hard disk assigned to this virtual machine.   | Integer   | No   |
| Virtual Machine Name   | The name of the virtual machine as it will appear in the vSphere user interface.   | String   | No   |

## Create VM Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Relative ISO Image Path | The path of the CD ISO image containing the operating system installed on the virtual machine. This path is relative to the provided datastore path. | String   | No   |

## Create VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Datastore Path   | The path of the data store   | String   |
| Folder Path   | The path to the folder on the host computer where the virtual machine is stored.   | String   |
| Guest Operating System  | The name of the guest operating system installed on the virtual machine.   | String   |
| Host System Path   | The path of the host system.   | String   |
| Memory(MB)   | The amount of memory, in megabytes assigned to the virtual machine.   | Integer   |
| NIC 1   | The first virtual network adapter assigned to the virtual machine.   | String   |
| NIC 2   | The second virtual network adapter assigned to the virtual machine.   | String   |
| NIC 3   | The third virtual network adapter assigned to the virtual machine.   | String   |
| NIC 4   | The fourth virtual network adapter assigned to the virtual machine.   | String   |
| Power on after creation | Indicates whether to turn on the virtual machine after it's created.   | Boolean   |
| Relative ISO Image Path | The path of the CD ISO image containing the operating system installed on the virtual machine. | String   |
| Resource Pool Path   | The path to the resource pool used by the virtual machine.   | String   |
| Virtual Disk Size (GB)  | The size of the virtual hard disk assigned to this virtual machine.   | Integer   |
| Virtual Machine Name   | The name of the virtual machine as it appears in the vSphere user interface.   | String   |

## Configure the Create VM Activity

The following procedure describes the steps required to configure a Create VM activity.

1. From the **Activities** pane, drag a **Create VM** activity to the active runbook.

2. Double-click the **Create VM** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
