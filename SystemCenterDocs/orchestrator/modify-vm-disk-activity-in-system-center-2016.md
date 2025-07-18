---
title: Modify VM Disk Activity in System Center 2016
description: The Modify VM Disk activity is used in a runbook to attach a virtual disk to a different virtual device node within a virtual machine.
ms.custom: UpdateFrequency3
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: c1ad150f-e139-40b7-be6b-4908cc75c501
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: 'sc-orch-2016'
---
# Modify VM Disk activity in System Center 2016

The Modify VM Disk activity is used in a runbook to attach a virtual disk to a different virtual device node within a virtual machine. When targeting version vCenter 5.0 or greater, it can also be used to extend the disk size of the selected disk. The following tables list the required and optional properties and published data for this activity.

### Modify VM Disk activity required properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the virtual disk. | String   | Yes   |
| SCSI Bus Number | The SCSI bus number of the SCSI controller.   | Integer   | No   |
| SCSI Unit Key   | The SCSI unit key of the disk.   | Integer   | No   |

### Modify VM Disk activity optional properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| New Disk Size (GB)  | The desired size of the extended disk in gigabytes.   | Integer   | No   |
| New SCSI Bus Number | The SCSI bus number of the SCSI controller to which you want to attach the disk. | Integer   | No   |
| New SCSI Unit Key   | The new SCSI unit key of the disk.   | Integer   | No   |

### Modify VM Disk activity published data

| Element   | Description   | Value type |
|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the virtual disk.   | String   |
| New Disk Size (GB)  | The desired size of the extended disk in gigabytes.   | Integer   |
| New SCSI Bus Number | The SCSI bus number of the SCSI controller to which you want to attach the disk. | Integer   |
| New SCSI Unit Key   | The new SCSI unit key of the disk.   | Integer   |
| SCSI Bus Number   | The SCSI bus number of the SCSI controller to which the disk is attached.   | Integer   |
| SCSI Unit Key   | The SCSI unit key of the disk.   | String   |

## Configure the Modify VM Disk activity

To configure the Modify VM Disk Activity, follow these steps:

1.  From the **Activities** pane, drag a **Modify VM Disk** activity to the active runbook.

2.  Double-click the **Modify VM Disk** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**.

    2.  Select the VMware vSphere server connection that you want to use for this activity, and select **OK**.

    3.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis button **(...)** next to the text box to browse for a value.

        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
