---
title: Delete VM Activity
description: The Delete VM activity is used in a runbook to permanently delete a virtual machine and all of its associated files that has already been added to the VMware ESX server host.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: daa3d513-25e3-4fa4-896a-ffb3526b0ea8
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Delete VM Activity

Applies To: System Center 2016 - Orchestrator

The Delete VM activity is used in a runbook to permanently delete a virtual machine and all of its associated files that has already been added to the VMware ESX server host. Using the Delete VM activity is the same as selecting **Delete from disk** from the VMware VirtualCenter server console. This allows the runbook to delete a virtual machine that is no longer needed.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Delete VM Activity Required Properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| VM Path | The path to the virtual machine being deleted. | String   | Yes   |

### Delete VM Activity Optional Properties

No optional properties are provided for this activity.

### Delete VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| VM Path | The path to the virtual machine that was deleted | String   |

## Configuring the Delete VM Activity

The following procedure describes the steps required to configure a Delete VM activity.

#### To configure the Delete VM Activity

1.  From the **Activities** pane, drag a **Delete VM** activity to the active runbook.

2.  Double-click the **Delete VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
