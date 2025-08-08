---
title: Delete VM Disk Activity in System Center 2016
description: The Delete VM Disk activity is used in a runbook to remove or delete a virtual disk from a virtual machine that is controlled by the VMware vSphere server. It also lists the activity data.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 496a3586-5ecd-4dd4-a885-33988cfea717
author: jyothisuri
ms.author: jsuri
monikerRange: 'sc-orch-2016'
---
# Delete VM Disk Activity in System Center 2016

The Delete VM Disk activity is used in a runbook to remove or delete a virtual disk from a virtual machine that is controlled by the VMware vSphere server.

The following tables list the required and optional properties and the published data for this activity. The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Delete VM Disk Activity Required Properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   | Yes   |
| SCSI Bus Number  | The SCSI bus number of the SCSI controller.   | Integer   | No   |
| SCSI Unit Key   | The SCSI unit key of the SCSI controller.   | Integer   | No   |
| Delete Disk File | Determines if the underlying .vmdk file of the virtual disk will be deleted from the data store. A value of True removes the disk from the virtual machine and deletes the underlying .vmdk file. A value of False removes the disk but preserves the underlying .vmdk file. | Boolean   | Yes   |

## Delete VM Disk Activity Optional Properties

No optional properties are provided for this activity.

## Delete VM Disk Activity Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   |
| SCSI Bus Number  | The SCSI bus number of the SCSI controller.   | Integer   |
| SCSI Unit Key   | The SCSI unit key of the SCSI controller.   | Integer   |
| Delete Disk File | Determines if the underlying .vmdk file of the virtual disk will be deleted from the data store. A value of True removes the disk from the virtual machine and deletes the underlying .vmdk file. A value of False removes the disk but preserves the underlying .vmdk file. | Boolean   |

## Configure the Delete VM Disk Activity

The following procedure describes the steps required to configure a Delete VM Disk activity.

1. From the **Activities** pane, drag a **Delete VM Disk** activity to the active runbook.

2. Double-click the **Delete VM Disk** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**.

    2. Select the VMware vSphere server connection that you want to use for this activity, and select **OK**.

    3. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis button **(...)** next to the text box to browse for a value.

        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
