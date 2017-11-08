---
title: Get Resource Pool Properties Activity
description: The Get Resource Pool Properties activity is used in a runbook to retrieve all the runtime information and static configuration information for a resource pool.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ffdc4a8b-e875-437d-afa0-9a1a0f1007bf
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# Get Resource Pool Properties Activity

The Get Resource Pool Properties activity is used in a runbook to retrieve all the runtime information and static configuration information for a resource pool. This allows the runbook to retrieve the runtime information of a resource pool and populate a performance report.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get Resource Pool Properties Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| ResourcePool Path | The path to the resource pool. | String   | Yes   |

## Get Resource Pool Properties Activity Optional Properties

No optional properties are provided for this activity.

## Get Resource Pool Properties Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| CPUmaxUsage   | The maximum available CPU cycles for the resource pool (in megahertz).   | Integer   |
| CPUoverallUsage   | The amount of CPU cycles used by the resource pool and VMs (in megahertz).   | Integer   |
| CPUreservationUsed   | The amount of CPU cycles currently being used by the pool (in megahertz).   | Integer   |
| CPUreservationUsedforVm   | The amount of CPU cycles currently being used by the VMs (in megahertz).   | Integer   |
| CPUunreservedForPool   | The amount of CPU cycles not currently being used by the pool (in megahertz).   | Integer   |
| CPUunreservedforVm   | The amount of CPU cycles not currently being used by the VMs (in megahertz).   | Integer   |
| CpuSharesLevel   | CPU allocation shares level. Can be the preset levels Low, Normal, High, or Custom. If Custom, the allocation is described in the CPUShares property.   | String   |
| CpuShares   | The number of CPU Shares allocated. Set to -1 if CpuSharesLevel has a preset level.   | Integer   |
| CpuReservation   | The guaranteed CPU MHz allocation available to the resource pool.   | Integer   |
| CpuLimit   | The CPU MHz limit of the resource pool.   | Integer   |
| CpuExpandableReservation   | True if the amount of reserved CPU can grow beyond the value that is specified in CpuReservation   | Boolean   |
| CpuUnlimited   | True if the CPU usage is unlimited. Otherwise, False.   | Boolean   |
| MemoryExpandableReservation | True if the memory reservation can grow beyond the value specified in **MemoryReservation**.   | Boolean   |
| MemoryLimit   | The memory limit for the resource pool, in megabytes. Set to -1 if the memory usage is unlimited.   | Integer   |
| MemoryMaxUsage   | The maximum amount of RAM available (in bytes).   | Integer   |
| MemoryOverallUsage   | The amount of memory that is currently being used (in bytes).   | Integer   |
| MemoryReservation   | The guaranteed memory allocation that is available to the resource pool, in megabytes.   | Integer   |
| MemoryReservationUsed   | The amount of memory that is in use for the pool (in bytes).   | Integer   |
| MemoryReservationUsedForVm  | The amount of memory that is in use for the VMs (in bytes).   | Integer   |
| MemorySharesLevel   | Memory allocation shares level. Can be the preset levels Low, Normal, High or Custom. If set to Custom, the allocation is described in the **MemoryShares** property. | String   |
| MemoryShares   | The number of Memory Shares allocated. Set to -1 if **MemorySharesLevel** has a preset level.   | Integer   |
| MemoryUnlimited   | True, if the memory usage is unlimited. Otherwise, False.   | Boolean   |
| MemoryUnreservedForPool   | The amount of memory that is not in use for the pool (in bytes).   | Integer   |
| MemoryUnreservedForVm   | The amount of memory that is not in use for the VMs (in bytes).   | Integer   |
| Overall Health   | The overall health of the resource pool. Green indicates under committed; yellow indicates overcommitted, and red indicates inconsistent.   | String   |
| Resource Pool Path   | The path of the resource pool.   | String   |
| Virtual Machine Path   | The paths of all the virtual machines in the resource pool.   | String   |

## Configuring the Get Resource Pool Properties Activity

The following procedure describes the steps required to configure a Get Resource Pool Properties activity.

### To configure the Get Resource Pool Properties activity

1.  From the **Activities** pane, drag a **Get Resource Pool Properties** activity to the active runbook.

2.  Double-click the **Get Resource Pool Properties** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
