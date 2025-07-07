---
title: Reset VM activity
description: The Reset VM activity is used in a runbook to stop and restart a running virtual machine.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: b9b39a7f-c6c4-4871-9792-988d84e3434d
author: jyothisuri
ms.author: jsuri
robots: noindex
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Reset VM activity

The Reset VM activity is used in a runbook to stop and restart a running virtual machine. This allows the runbook to reset a virtual machine of a VMware vSphere server that's no longer responding to ping commands.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Reset VM activity required properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path of the virtual machine to be reset. | String   | Yes   |

### Reset VM activity optional properties

No optional properties are provided for this activity.

### Reset VM activity published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| VM Path | The path of the virtual machine. | String   |

## Configure the Reset VM activity

To configure the Reset VM activity, follow these steps:

1.  From the **Activities** pane, drag a **Reset VM** activity to the active runbook.

2.  Double-click the **Reset VM** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
