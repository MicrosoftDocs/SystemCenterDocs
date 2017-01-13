---
title: Stop VM Activity
description: The Stop VM activity is used in a runbook to stop a virtual machine that has already been added to a VMware vSphere server.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 805be22b-4cb4-4cc0-96f4-3f20d38bd989
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Stop VM Activity

Applies To: System Center 2016 - Orchestrator

The Stop VM activity is used in a runbook to stop a virtual machine that has already been added to a VMware vSphere server. This allows the runbook to stop a virtual machine before deleting it using the Delete VM activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Stop VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
| Gracefully shutdown | Indicates whether the guest operating system is shut down instead of powered off. | Boolean   | Yes   |
|:---|:---|:---|:---|
| VM Path   | The path to the virtual machine.   | String   | Yes   |

### Stop VM Activity Optional Properties

|   |
|--------------------------------------------------------|
| No optional properties are provided for this activity. |

### Stop VM Activity Published Data

| Name   | Description   | Value Type |
| Gracefully shut down | Indicates whether the guest operating system is shut down instead of powered off. | Boolean   |
|:---|:---|:---|
| VM Path   | The path to the virtual machine.   | String   |

## Configuring the Stop VM Activity

The following procedure describes the steps required to configure a Stop VM activity.

#### To configure the Stop VM Activity

1.  From the **Activities** pane, drag a **Stop VM** activity to the active runbook.

2.  Double-click the **Stop VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


