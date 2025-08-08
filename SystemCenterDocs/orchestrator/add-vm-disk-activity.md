---
title: Add VM Disk Activity
description: The Add VM Disk activity is used in a runbook to add a virtual disk to a virtual machine controlled by the VMware vSphere server.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 08f66280-43b4-4f32-ae2d-97936c2bdb1f
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Add VM Disk Activity

The Add VM Disk activity is used in a runbook to add a virtual disk to a virtual machine controlled by the VMware vSphere server. This can be used to increase the amount of disk space allocated to an existing virtual machine.

::: moniker range="sc-orch-2016"

For System Center 2016: If a SCSI controller isn't associated with the SCSI bus number specified in the activity, choosing a SCSI controller type will add a new controller and attach the new disk to it.

::: moniker-end

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Add VM Disk Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Disk size (GB) | The disk size in gigabytes to allocate to the virtual machine disk. | Integer   | No   |
| VM Path   | The path of the source virtual machine.   | String   | Yes   |

### Add VM Disk Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Datastore   | The path of the data store that will hold the new disk.   | String   | No   |
| SCSI Bus Number   | The SCSI bus number of the SCSI controller   | Integer   | No   |
| SCSI Unit Key   | The SCSI unit key of the SCSI controller   | Integer   | No   |
| SCSI Controller Type | The type of SCSI controller to add if one doesn't exist on the chosen SCSI bus. | String   | Yes   |

### Add VM Disk Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Datastore   | The datastore that holds the disk that was added.   | String   |
| Disk size (GB)   | The amount of disk size in gigabytes allocated to the virtual machine.   | Integer   |
| SCSI Bus Number   | The SCSI bus number setting specified.  | Integer   |
| SCSI Unit Key   | The SCSI unit key setting specified.   | Integer   |
| VM Path   | The path of the virtual machine that this disk belongs to.   | String   |
| SCSI Controller Type | The type of SCSI controller to add if one doesn't exist on the chosen SCSI bus. | String   |

## Configure the Add VM Disk Activity

The following procedure describes the steps required to configure an Add VM Disk activity.

1. From the **Activities** pane, drag an **Add VM Disk** activity to the active runbook.

2. Double-click the **Add VM Disk** activity icon.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use the published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
