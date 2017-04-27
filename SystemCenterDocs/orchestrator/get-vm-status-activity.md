---
title: Get VM Status Activity
description: The Get VM Status activity is used in a runbook to retrieve the state and other related information about a virtual machine.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 912dfce9-c159-4de2-853b-c47fc161b5ca
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Get VM Status Activity

Applies To: System Center 2016 - Orchestrator

The Get VM Status activity is used in a runbook to retrieve the state and other related information about a virtual machine. This, for example, enables the runbook to retrieve the current status of a virtual machine to ensure that is has been properly shut down before performing a backup.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get VM Status Activity Required Properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path of the virtual machine to retrieve the status for. | String   | Yes   |


## Get VM Status Activity Optional Properties
No optional properties are provided for this activity.

## Get VM Status Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| CPU Usage   | The current CPU usage of the virtual machine   | Integer   |
| Computer Name   | The computer name assigned to the guest operating system.   | String   |
| Disk Capacity(MB) | The size of the virtual disk in megabytes.   | Integer   |
| IP Address   | The primary IP address of the virtual machine.   | String   |
| Memory Size (MB)  | The amount of memory assigned to the virtual machine in megabytes.   | Integer   |
| Name   | The name of the virtual machine.   | String   |
| Network List   | The list of networks that this virtual machine is connected to.   | String   |
| Number of CPU   | The number of CPUs that are assigned to this virtual machine.   | Integer   |
| Physical Path   | The path on the file system where the virtual machine configuration file can be found. | String   |
| Power State   | The current power state of the virtual machine.   | String   |
| VM Folder   | The vCenter managed folder containing this virtual machine.   | String   |
| VM OS Full Name   | The full name of the guest operating system.   | String   |
| VM Path   | The full path of the virtual machine on the vCenter server.   | String   |
| VM UUID   | The UUID of the virtual machine as assigned by the vCenter server.   | String   |

## Configuring the Get VM Status Activity

The following procedure describes the steps required to configure a Get VM Status activity.

### To configure the Get VM Status Activity

1.  From the **Activities** pane, drag a **Get VM Status** activity to the active runbook.

2.  Double-click the **Get VM Status** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
