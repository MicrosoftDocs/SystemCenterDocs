---
title: Modify VM Disk Activity
description: This article describes how the Modify VM Disk activity is used in a runbook to attach a virtual disk to a different virtual device node within a virtual machine.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: how-to
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 04/22/2025
---

# Modify VM Disk activity

This article describes how the Modify VM Disk activity is used in a runbook to attach a virtual disk to a different virtual device node within a virtual machine. When targeting version vCenter 5.0 or greater, it can also be used to extend the disk size of the selected disk.

The following tables list the required and optional properties and published data for this activity.

## Required properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the virtual disk. | String   | Yes   |
| SCSI Bus Number | The SCSI bus number of the SCSI controller.   | Integer   | No   |
| SCSI Unit Key   | The SCSI unit key of the disk.   | Integer   | No   |

## Optional properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| New Disk Size (GB)  | The desired size of the extended disk in gigabytes.   | Integer   | No   |
| New SCSI Bus Number | The SCSI bus number of the SCSI controller to which you want to attach the disk. | Integer   | No   |
| New SCSI Unit Key   | The new SCSI unit key of the disk.   | Integer   | No   |

## Published data

| Element   | Description   | Value type |
|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the virtual disk.   | String   |
| New Disk Size (GB)  | The desired size of the extended disk in gigabytes.   | Integer   |
| New SCSI Bus Number | The SCSI bus number of the SCSI controller to which you want to attach the disk. | Integer   |
| New SCSI Unit Key   | The new SCSI unit key of the disk.   | Integer   |
| SCSI Bus Number   | The SCSI bus number of the SCSI controller to which the disk is attached.   | Integer   |
| SCSI Unit Key   | The SCSI unit key of the disk.   | String   |

## Configure the activity

To configure the activity, follow these steps:

1. From the **Activities** pane, drag a **Modify VM Disk** activity to the active runbook.

2. Double-click the **Modify VM Disk** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**.

    2. Select the VMware vSphere server connection that you want to use for this activity, and select **OK**.

    3. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.

        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
