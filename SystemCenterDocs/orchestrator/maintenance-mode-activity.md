---
title: Maintenance Mode activity
description: The Maintenance Mode activity is used in a runbook to enter and exit maintenance mode for an ESX host controlled by the VMware vSphere vCenter server.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: d6bff75f-98f3-4156-a740-b190fcedbafd
author: jyothisuri
ms.author: jsuri
robots: noindex
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Maintenance Mode activity

The Maintenance Mode activity is used in a runbook to enter and exit the maintenance mode for an ESX host controlled by the VMware vSphere vCenter server. Entering the maintenance mode prevents VMs powering up or failing over to the host if it's taking part in a high availability cluster. This allows the runbook to enable the Maintenance mode before powering off the host for hardware maintenance.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Maintenance Mode activity required properties

| Element   | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Host   | The path of the managed host controlled by the vSphere VMware server. | String   | Yes   |
| Operation | The action that is to be performed, selected from a dropdown list.   | Enter causes the host to enter maintenance mode.<br>Exit causes the host to exit maintenance mode. | Yes   |

### Maintenance Mode activity optional properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Evacuate Powered Off VMs | If true, the activity won't succeed on a non-DRS cluster unless all powered-off virtual machines have been manually reregistered.<br>On a DRS-enabled cluster, vCenter will automatically reregister powered-off virtual machines. | Boolean   | Yes   |
| Timeout (Seconds)   | The time in seconds for the operation to complete.   | Integer   | No   |

### Maintenance Mode activity published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Host   | The path of the managed host controlled by the vSphere VMware server.   | String   |
| Operation   | The action that is to be performed, selected from a drop-down list.   | String   |
| Evacuate Powered Off VMs | If true, the activity won't succeed on a non-DRS cluster unless all powered-off virtual machines have been manually reregistered. On a DRS-enabled cluster, vCenter will automatically reregister powered off virtual machines. | Boolean   |
| Timeout (Seconds)   | The time in seconds for the operation to complete.   | Integer   |

## Configure the Maintenance Mode activity

The following procedure describes the steps required to configure a Maintenance Mode activity.

1. From the **Activities** pane, drag a **Maintenance Mode** activity to the active runbook.

2. Double-click the **Maintenance Mode** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2. In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4. Select **Finish**.
