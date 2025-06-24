---
title: Get Resource Pools Activity
description: The Get Resource Pools activity is used in a runbook to retrieve a list of all the resource pools in managed by the VMware vSphere system.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 662fa33f-d507-4721-9369-b5c2ad518731
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
---

# Get Resource Pools Activity

The Get Resource Pools activity is used in a runbook to retrieve a list of all the resource pools in managed by the VMware vSphere system. This allows the runbook to retrieve the resources pools before using the Get Resource Pool Runtime Info Activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get Resource Pools Activity Required Properties

No required properties are provided for this activity.

## Get Resource Pools Activity Optional Properties

No optional properties are provided for this activity.

## Get Resource Pools Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Resource Pool | A list of resource pool paths within the vCenter server. | String   |

## Configure the Get Resource Pools Activity

To configure the Get Resource Pools Activity, follow these steps:

1. From the **Activities** pane, drag a **Get Resource Pools** activity to the active runbook.

2. Double-click the **Get Resource Pools** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.

4. Select **Finish**.
