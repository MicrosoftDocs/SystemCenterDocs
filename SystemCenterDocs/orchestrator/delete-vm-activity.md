---
title: Delete VM Activity
description: The Delete VM activity is used in a runbook to permanently delete a virtual machine and all of its associated files that has already been added to the VMware ESX server host.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: daa3d513-25e3-4fa4-896a-ffb3526b0ea8
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Delete VM Activity

The Delete VM activity is used in a runbook to permanently delete a virtual machine and all its associated files that have already been added to the VMware ESX server host. Using the Delete VM activity is the same as selecting **Delete from disk** from the VMware VirtualCenter server console. This allows the runbook to delete a virtual machine that's no longer needed.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Delete VM Activity Required Properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path to the virtual machine being deleted. | String   | Yes   |

## Delete VM Activity Optional Properties

No optional properties are provided for this activity.

## Delete VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| VM Path | The path to the virtual machine that was deleted | String   |

## Configure the Delete VM Activity

The following procedure describes the steps required to configure a Delete VM activity.

1. From the **Activities** pane, drag a **Delete VM** activity to the active runbook.

2. Double-click the **Delete VM** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
