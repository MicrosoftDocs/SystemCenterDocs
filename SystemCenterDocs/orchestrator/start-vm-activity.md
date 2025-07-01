---
title: Start VM Activity
description: The Start VM activity is used in a runbook to start a virtual machine that has been added to a VMware vSphere server and is not already running.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: f16bf32e-0018-4d47-96c4-a90a79d1d37f
author: jyothisuri
ms.author: jsuri
robots: noindex
ms.date: 11/01/2024
---
# Start VM Activity

The Start VM activity is used in a runbook to start a virtual machine that has been added to a VMware vSphere server and isn't already running. The Start VM activity waits for the guest operating system to complete its boot up sequence before continuing to the next object in the runbook. This allows the runbook to start a virtual machine after it has been paused by the Suspend VM activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Start VM Activity Required Properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path of the virtual machine to be started. | String   | Yes   |

## Start VM Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Timeout (seconds) | The time allowed for the start operation to complete. | Integer   | No   |

## Start VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| VM Path | The path of the virtual machine that was started. | String   |

## Configure the Start VM Activity

To configure the Start VM activity, follow these steps:

1.  From the **Activities** pane, drag a **Start VM** activity to the active runbook.

2.  Double-click the **Start VM** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
