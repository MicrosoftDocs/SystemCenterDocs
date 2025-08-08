---
title: Get Hosts Activity
description: The Get Hosts activity is used in a runbook to retrieve all the hosts attached to a vCenter instance.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 25a60cd2-3942-47f6-b671-e126f109d291
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
---

# Get Hosts Activity

The Get Hosts activity is used in a runbook to retrieve all the hosts attached to a vCenter instance. This allows the runbook to determine the list of hosts before cloning or creating virtual machines on a designated host.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get Hosts Activity Required Properties

No required properties are provided for this activity.

## Get Hosts Activity Optional Properties

No optional properties are provided for this activity.

## Get Hosts Activity Published Data

| Name | Description                                         | Value Type |
|:-----|:----------------------------------------------------|:-----------|
| Host | A list of host paths managed by the vCenter server. | String     |

To configure the Get Hosts Activity, follow these steps:

1. From the **Activities** pane, drag a **Get Hosts** activity to the active runbook.

2. Double-click the **Get Hosts** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.

4. Select **Finish**.
