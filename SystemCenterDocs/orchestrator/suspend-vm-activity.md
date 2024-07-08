---
title: Suspend VM Activity
description: The Suspend VM activity is used in a runbook to suspend a virtual machine that has already been added to a VMware vSphere server and is already running.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 867cfa59-95c4-403c-a5a8-280ec43dc18b
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
ms.date: 07/08/2024
---
# Suspend VM Activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Suspend VM activity is used in a runbook to suspend a virtual machine that has already been added to a VMware vSphere server and is already running. This, for example, enables the runbook to suspend a running virtual machine before backing it up. Then use the Start VM activity to start it again.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Suspend VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Enter standby mode | Indicates that the guest operating system will be put in the standby mode. If the standby mode isn't supported by the guest operating system, this option will be ignored. | Boolean   | Yes   |
| VM Path   | The path to the virtual machine to be suspended.   | String   | Yes   |

## Suspend VM Activity Optional Properties

No optional properties are provided for this activity.

## Suspend VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Enter standby mode | Indicates whether the Enter standby mode option was selected. | Boolean   |
| VM Path   | The path to the virtual machine that was suspended.   | String   |

## Configuring the Suspend VM Activity

The following procedure describes the steps required to configure a Suspend VM activity.

### To configure the Suspend VM Activity

1.  From the **Activities** pane, drag a **Suspend VM** activity to the active runbook.

2.  Double-click the **Suspend VM** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
