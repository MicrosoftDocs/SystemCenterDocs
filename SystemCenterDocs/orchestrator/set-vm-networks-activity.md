---
title: Set VM Networks Activity
description: The Set VM Networks activity is used in a runbook to replace the first virtual machine network switch with one that is specified.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5866dc7c-6edb-42ab-ada0-720994e912c5
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
ms.date: 07/10/2024
---
# Set VM Networks Activity

The Set VM Networks activity is used in a runbook to replace the first virtual machine network switch with one that is specified. This allows the runbook to change the network switch that a virtual machine is using.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Set VM Networks Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Network Adapter 1 | The name of the network that the first network adapter is attached to.  | String   | Yes   |
| Network Adapter 2 | The name of the network that the second network adapter is attached to. | String   | Yes   |
| Network Adapter 3 | The name of the network that the third network adapter is attached to.  | String   | Yes   |
| Network Adapter 4 | The name of the network that the fourth network adapter is attached to. | String   | Yes   |
| VM Path   | The path to the virtual machine.   | String   | Yes   |

## Set VM Networks Activity Optional Properties

No optional properties are provided for this activity.

## Set VM Networks Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Network Adapter 1 | The name of the network that the first network adapter is attached to.  | String   |
| Network Adapter 2 | The name of the network that the second network adapter is attached to. | String   |
| Network Adapter 3 | The name of the network that the third network adapter is attached to.  | String   |
| Network Adapter 4 | The name of the network that the fourth network adapter is attached to. | String   |
| VM Path   | The path to the virtual machine.   | String   |

## Configure the Set VM Networks Activity

To configure the Set VM Networks Activity, follow these steps:

1.  From the **Activities** pane, drag a **Set VM Networks** activity to the active runbook.

2.  Double-click the **Set VM Networks** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
