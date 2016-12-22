---
title: Revert VM Snapshot Activity
description: The Revert VM Snapshot activity is used in a runbook to revert a virtual machine to the last available snapshot.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8b03da9-f448-44bd-b8e2-d87b809d4d92
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Revert VM Snapshot Activity
===========================

Applies To: System Center 2016 - Orchestrator

The Revert VM Snapshot activity is used in a runbook to revert a virtual machine to the last available snapshot. This allows the runbook to revert a snapshot to its previous state after you have finished using it.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Revert VM Snapshot Activity Required Properties

| Element | Description   | Valid Values | Look up |
| VM Path | The path of the VM to be reverted. | String   | Yes   |
|:---|:---|:---|:---|

### Revert VM Snapshot Activity Optional Properties

| Name   | Description   | Valid Values | Look up |
| Revert to Snapshot | The path of the snapshot to be reverted. | String   | No   |
|:---|:---|:---|:---|

### Revert VM Snapshot Activity Published Data

| Name   | Description   | Value Type |
| VM Path   | The path of the VM that was reverted.   | String   |
|:---|:---|:---|
| Revert to Snapshot | The path of the snapshot that was reverted. | String   |

Configuring the Revert VM Snapshot Activity
-------------------------------------------

The following procedure describes the steps required to configure a Revert VM Snapshot activity.

#### To configure the Revert VM Snapshot Activity

1.  From the **Activities** pane, drag a **Revert VM Snapshot** activity to the active runbook.

2.  Double-click the **Revert VM Snapshot** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


