---
title: Delete Network Adapter Activity in System Center 2016
description: The Delete Network Adapter activity is used in a runbook to remove a virtual network adapter from a virtual machine controlled by the VMware vSphere server.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1cf6a81-0362-4d5d-8019-f53605311470
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Delete Network Adapter Activity in System Center 2016

Applies To: System Center 2016 - Orchestrator

The Delete Network Adapter activity is used in a runbook to remove a virtual network adapter from a virtual machine controlled by the VMware vSphere server. The network adapter to remove is identified by its MAC address. A list of MAC addresses associated with a virtual machine can be found using the Get VM Properties activity.

The following tables list the required and optional properties and the published data for this activity. The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Delete Network Adapter Activity Required Properties

| Element   | Description   | Valid values | Look up |
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   | Yes   |
|:---|:---|:---|:---|
| MAC Address | The MAC address of the network adapter to remove. The formats "00:11:22:33:44:55" and "00-11-22-33-44-55" are accepted. | String   | No   |

### Delete Network Adapter Activity Optional Properties

|   |
|--------------------------------------------------------|
| No optional properties are provided for this activity. |

### Delete Network Adapter Activity Published Data

| Element   | Description   | Value Type |
| VM Path   | The path of the virtual machine containing the adapter to delete.   | String   |
|:---|:---|:---|
| MAC Address | The MAC address of the network adapter to remove. The formats "00:11:22:33:44:55" and "00-11-22-33-44-55" are accepted. | String   |

## To Configure the Delete Network Adapter Activity

The following procedure describes the steps required to configure a Delete Network Adapter activity.

#### To configure the Delete Network Adapter Activity

1.  From the **Activities** pane, drag a **Delete Network Adapter** activity to the active runbook.

2.  Double-click the **Delete Network Adapter** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**.

    2.  Select the VMware vSphere server connection that you want to use for this activity, and then click **OK**.

    3.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.

        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


