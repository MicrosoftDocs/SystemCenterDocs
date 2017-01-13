---
title: Get Host Properties Activity
description: The Get Host Properties activity is used in a runbook to retrieve a list of properties for a specified host in the VMware vSphere cluster.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32e0b1e4-6e53-42a3-a6e1-4f144d2e4073
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Host Properties Activity

Applies To: System Center 2016 - Orchestrator

The Get Host Properties activity is used in a runbook to retrieve a list of properties for a specified host in the VMware vSphere cluster. Examples of these properties include Connection Status (Powered on, disconnected, etc) and Maintenance Mode state.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Get Host Properties Activity Required Properties

| Element | Description   | Valid Values | Look up |
| Host   | The name of the managed host controlled by the VMware vCenter server | String   | Yes   |
|:---|:---|:---|:---|

### Get Host Properties Activity Optional Properties

|   |
|-------------------------------------------------------|
| No optional properties are provided for this activity |

### Get Host Properties Activity Published Data

| Name   | Description   | Value Type   |
| Connection State   | The connection state of the host.   | Connected<br> Not Responding<br> Disconnected   |
|:---|:---|:---|
| Host   | The identifier of the host.   | String   |
| In Maintenance Mode | Indicates whether the host is in maintenance mode.   | True@br False   |
| Name   | The name of the managed host.   | String   |
| Overall Status   | The overall status of the host.   | Gray (unknown)@br Green (OK)@br Yellow (warning)@br Red (alarm)   |
| Port   | The management port for the managed host.   | Integer   |
| Power State   | The power state of the host.   | Powered On@br Powered Off@br Standby@br Unknown (e.g. disconnected) |
| Product   | The full product name and version of the host hypervisor. | String   |
| Reboot Required   | Indicates whether a reboot is required.   | True@br False   |
| vMotion Enabled   | Indicates whether vMotion is enabled.   | True@br False   |

## Configuring the Get Host Properties Activity

The following procedure describes the steps required to configure a Get Host Properties activity.

#### To configure the Get Host Properties Activity

1.  From the **Activities** pane, drag a **Get Host Properties** activity to the active runbook.

2.  Double-click the **Get Host Properties** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


