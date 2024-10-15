---
title: Revert VM Snapshot activity
description: The Revert VM Snapshot activity is used in a runbook to revert a virtual machine to the last available snapshot.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8b03da9-f448-44bd-b8e2-d87b809d4d92
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
ms.date: 11/01/2024
---
# Revert VM Snapshot activity

The Revert VM Snapshot activity is used in a runbook to revert a virtual machine to the last available snapshot. This allows the runbook to revert a snapshot to its previous state after you've finished using it.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Revert VM Snapshot activity required properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path of the VM to be reverted. | String   | Yes   |

### Revert VM Snapshot activity optional properties

| Name   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Revert to Snapshot | The path of the snapshot to be reverted. | String   | No   |

### Revert VM Snapshot activity published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| VM Path   | The path of the VM that was reverted.   | String   |
| Revert to Snapshot | The path of the snapshot that was reverted. | String   |

## Configuring the Revert VM Snapshot activity

The following procedure describes the steps required to configure a Revert VM Snapshot activity.

#### Configure the Revert VM Snapshot activity

1.  From the **Activities** pane, drag a **Revert VM Snapshot** activity to the active runbook.

2.  Double-click the **Revert VM Snapshot** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
