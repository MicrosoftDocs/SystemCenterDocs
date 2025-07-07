---
title: Delete Network Adapter Activity in System Center
description: The Delete Network Adapter activity is used in a runbook to remove a virtual network adapter from a virtual machine controlled by the VMware vSphere server. The network adapter to remove is identified by its MAC address.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: a1cf6a81-0362-4d5d-8019-f53605311470
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: 'sc-orch-2016'
---

# Delete Network Adapter Activity in System Center

The Delete Network Adapter activity is used in a runbook to remove a virtual network adapter from a virtual machine controlled by the VMware vSphere server. The network adapter to remove is identified by its MAC address. A list of MAC addresses associated with a virtual machine can be found using the Get VM Properties activity.

The following tables list the required and optional properties and the published data for this activity. The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Delete Network Adapter Activity Required Properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   | Yes   |
| MAC Address | The MAC address of the network adapter to remove. The formats **00:11:22:33:44:55** and **00-11-22-33-44-55** are accepted. | String   | No   |

## Delete Network Adapter Activity Optional Properties

No optional properties are provided for this activity.

## Delete Network Adapter Activity Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   |
| MAC Address | The MAC address of the network adapter to remove. The formats **00:11:22:33:44:55** and **00-11-22-33-44-55** are accepted. | String   |

## Configure the Delete Network Adapter Activity

1. From the **Activities** pane, drag a **Delete Network Adapter** activity to the active runbook.

2. Double-click the **Delete Network Adapter** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**.

    2. Select the VMware vSphere server connection that you want to use for this activity, and select **OK**.

    3. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis button **(...)** next to the text box to browse for a value.

        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
