---
title: Start VM Activity
description: The Start VM activity is used in a runbook to start a virtual machine that has been added to a VMware vSphere server and is not already running.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f16bf32e-0018-4d47-96c4-a90a79d1d37f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Start VM Activity

Applies To: System Center 2016 - Orchestrator

The Start VM activity is used in a runbook to start a virtual machine that has been added to a VMware vSphere server and is not already running. The Start VM activity waits for the guest operating system to complete its boot up sequence before continuing to the next object in the runbook. This allows the runbook to start a virtual machine after it has been paused by the Suspend VM activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Start VM Activity Required Properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path of the virtual machine to be started. | String   | Yes   |

### Start VM Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Timeout (seconds) | The time allowed for the start operation to complete. | Integer   | No   |

### Start VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| VM Path | The path of the virtual machine that was started. | String   |

## Configuring the Start VM Activity

The following procedure describes the steps required to configure a Start VM activity.

#### To configure the Start VM activity

1.  From the **Activities** pane, drag a **Start VM** activity to the active runbook.

2.  Double-click the **Start VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
