---
title: Add Network Adapter Activity
description: The Add Network Adapter activity is used in a runbook to add a virtual network adapter to a virtual machine controlled by the VMware vSphere server.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b09506e-34d1-4c32-ad34-600d86ceb109
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Add Network Adapter Activity

Applies To: System Center 2016 - Orchestrator

The **Add Network Adapter** activity is used in a runbook to add a virtual network adapter to a virtual machine controlled by the VMware vSphere server. This can be used to connect the virtual machine to multiple networks in a multi-homed environment or to add the first network adapter as part of a provisioning process.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Add Network Adapter Activity Required Properties

| Element   | Description   | Valid Values | Look up |
| Adapter Type   | The virtual network adapter type. For System Center 2016, the supported types are **Flexible**, **VMXNET 2 (Enhanced)**, **VMXNET 3** and **E1000**. | String   | Yes   |
|:---|:---|:---|:---|
| Connection at Power On | Indicates whether the adapter will be connected when the virtual machine is powered on.   | Boolean   | Yes   |
| Network   | The vSphere network that the adapter will connect to.   | String   | Yes   |
| VM Path   | The path of the virtual machine.   | String   | Yes   |

### Add Network Adapter Activity Optional Properties

|   |
|--------------------------------------------------------|
| No optional properties are provided for this activity. |

### Add Network Adapter Activity Published Data

| Name   | Description   | Value Type |
| Adapter type   | The selected adapter type   | String   |
|:---|:---|:---|
| Connection at Power On | Whether the adapter will be connected when the virtual machine is powered on | Boolean   |
| Network   | The network that the adapter is connected to   | String   |
| VM path   | The path of the virtual machine that the adapter belongs to   | String   |

## Configuring the Add Network Adapter Activity

The following procedure describes the steps required to configure an Add Network Adapter activity.

#### To configure the Add Network Adapter Activity

1.  From the **Activities** pane, drag an **Add Network Adapter** activity to the active runbook.

2.  Double-click the **Add Network Adapter Activity** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


