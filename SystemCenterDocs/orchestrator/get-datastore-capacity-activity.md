---
title: Get Datastore Capacity Activity
description: The Get Datastore Capacity activity is used in a runbook to retrieve the capacity available on a specific data store.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 1c02fe50-cf8c-4451-984b-b1bda2b9fb0a
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---

# Get Datastore Capacity Activity

The Get Datastore Capacity activity is used in a runbook to retrieve the capacity available on a specific data store. This allows the runbook to retrieve the available capacity of a data store before cloning or creating virtual machines in the data store.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get Datastore Capacity Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Datastore | The name of the data store for which to retrieve the capacity. | String   | No   |

## Get Datastore Capacity Activity Optional Properties

No optional properties are provided for this activity.

## Get Datastore Capacity Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Capacity   | The total capacity of the data store.   | Integer   |
| Free Space   | The total amount of available space.   | Integer   |
| Percent Free | The amount of available space as a percentage of the available capacity. | Integer   |

## Configure the Get Datastore Capacity Activity

To configure the Get Datastore Capacity Activity, follow these steps:

1. From the **Activities** pane, drag a **Get Datastore Capacity** activity to the active runbook.
2. Double-click the **Get Datastore Capacity** activity icon. The **Properties** dialog opens.
3. Configure the settings in the **Properties** tab as follows:
    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.
4. Select **Finish**.
