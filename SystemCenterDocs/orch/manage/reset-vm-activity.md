---
title: Reset VM Activity
description: The Reset VM activity is used in a runbook to stop and restart a running virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b39a7f-c6c4-4871-9792-988d84e3434d
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Reset VM Activity

Applies To: System Center 2016 - Orchestrator

The Reset VM activity is used in a runbook to stop and restart a running virtual machine. This allows the runbook to reset a virtual machine of a VMware vSphere server that is no longer responding to ping commands.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Reset VM Activity Required Properties

| Element | Description   | Valid Values | Look up |
| VM Path | The path of the virtual machine to be reset. | String   | Yes   |
|:---|:---|:---|:---|

### Reset VM Activity Optional Properties

|   |
|-------------------------------------------------------|
| No optional properties are provided for this activity |

### Reset VM Activity Published Data

| Name   | Description   | Value Type |
| VM Path | The path of the virtual machine. | String   |
|:---|:---|:---|

## Configuring the Reset VM Activity

The following procedure describes the steps required to configure a Reset VM activity.

#### To configure the Reset VM Activity

1.  From the **Activities** pane, drag a **Reset VM** activity to the active runbook.

2.  Double-click the **Reset VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


