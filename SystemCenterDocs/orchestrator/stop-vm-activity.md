---
title: Stop VM Activity
description: The Stop VM activity is used in a runbook to stop a virtual machine that has already been added to a VMware vSphere server.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 805be22b-4cb4-4cc0-96f4-3f20d38bd989
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
ms.date: 07/10/2024
---
# Stop VM Activity

The Stop VM activity is used in a runbook to stop a virtual machine that has already been added to a VMware vSphere server. This allows the runbook to stop a virtual machine before deleting it using the Delete VM activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Stop VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Gracefully shutdown | Indicates whether the guest operating system is shut down instead of powered off. | Boolean   | Yes   |
| VM Path   | The path to the virtual machine.   | String   | Yes   |

## Stop VM Activity Optional Properties

No optional properties are provided for this activity.

## Stop VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Gracefully shut down | Indicates whether the guest operating system is shut down instead of powered off. | Boolean   |
| VM Path   | The path to the virtual machine.   | String   |

## Configure the Stop VM Activity

To configure the Stop VM Activity, follow these steps:

1.  From the **Activities** pane, drag a **Stop VM** activity to the active runbook.

2.  Double-click the **Stop VM** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
