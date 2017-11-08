---
title: Take VM Snapshot Activity
description: The Take VM Snapshot activity is used in a runbook to take a snapshot of a running virtual machine on a VMware vSphere server and enable a new name and description to be assigned to the snapshot.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c5412de-82b9-49e0-98f4-31d974ac0b83
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Take VM Snapshot Activity

The Take VM Snapshot activity is used in a runbook to take a snapshot of a running virtual machine on a VMware vSphere server and enable a new name and description to be assigned to the snapshot. This allows the runbook to create a new virtual machine based on the configuration of an existing one.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Take VM Snapshot Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Snapshot Name   | A name for the snapshot being created.   | String   | No   |
| Snapshot VM Memory | Indicates whether the source virtual machine's memory is included in the snapshot | Boolean   | Yes   |
| VM Path   | The path to the virtual machine to take a snapshot of   | String   | Yes   |

## Take VM Snapshot Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Snapshot Description | A description of the snapshot to be created. | String   | No   |

## Take VM Snapshot Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Snapshot Description | A description of the snapshot that was created.   | String   |
| Snapshot Name   | The name of the snapshot.   | String   |
| Snapshot VM Memory   | Indicates whether the source virtual machine's memory was included in the snapshot. | Boolean   |
| VM Path   | The path to the virtual machine from which the snapshot was taken.   | String   |

## Configuring the Take VM Snapshot Activity

The following procedure describes the steps required to configure a Take VM Snapshot activity.

### To configure the Take VM Snapshot activity

1.  From the **Activities** pane, drag a **Take VM Snapshot** activity to the active runbook.

2.  Double-click the **Take VM Snapshot** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
