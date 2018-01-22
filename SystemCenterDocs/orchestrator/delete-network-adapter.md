---
title: Delete Network Adapter Activity in System Center - Orchestra
description: The Delete Network Adapter activity is used in a runbook to remove a virtual network adapter from a virtual machine controlled by the VMware vSphere server.
ms.date: 01/22/2018
ms.prod: system-center-threshold
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---
# Delete Network Adapter activity 

The Delete Network Adapter activity is used in a runbook to remove a virtual network adapter from a virtual machine controlled by the VMware vSphere server. The network adapter to remove is identified by its MAC address. A list of MAC addresses associated with a virtual machine can be found using the Get VM Properties activity.

The following tables list the required and optional properties and the published data for this activity. The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Required properties

| Element   | Description   | Valid values | Look up |
|:---|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   | Yes   |
| MAC Address | The MAC address of the network adapter to remove. The formats "00:11:22:33:44:55" and "00-11-22-33-44-55" are accepted. | String   | No   |

### Optional properties

No optional properties are provided for this activity.

### Published data

| Element   | Description   | Value Type |
|:---|:---|:---|
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   |
| MAC Address | The MAC address of the network adapter to remove. The formats "00:11:22:33:44:55" and "00-11-22-33-44-55" are accepted. | String   |

## Configure the activity

1.  From the **Activities** pane, drag a **Delete Network Adapter** activity to the active runbook.

2.  Double-click the **Delete Network Adapter** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**.

    2.  Select the VMware vSphere server connection that you want to use for this activity, and then click **OK**.

    3.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.

        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
