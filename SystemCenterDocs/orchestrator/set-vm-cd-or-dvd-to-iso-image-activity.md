---
title: Set VM CD or DVD to ISO Image Activity
description: The Set VM CD/DVD to ISO Image activity is used in a runbook to set the CD/DVD drive of a virtual machine to an ISO image.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: ec4ce381-6145-4af2-bfde-51f461e3d9b7
author: jyothisuri
ms.author: jsuri
robots: noindex
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Set VM CD or DVD to ISO Image Activity

The Set VM CD/DVD to ISO Image activity is used in a runbook to set the CD/DVD drive of a virtual machine to an ISO image. This allows the runbook to attach a CD/DVD image of a software application for automatic provisioning.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Set VM CD/DVD to ISO Image Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Datastore   | The path of the datastore that contains the ISO image.   | String   | No   |
| Relative File Path | The path to the ISO image relative to the host and datastore. | String   | No   |
| VM Path   | The path to the virtual machine.   | String   | Yes   |

## Set VM CD/DVD to ISO Image Activity Optional Properties

No optional properties are provided for this activity.

## Set VM CD/DVD to ISO Image Activity Published Data

| Name   | Description   | Valid Values |
|:---|:---|:---|
| Datastore | The path of the datastore that contains the ISO image. | String   |
| VM Path   | The path to the virtual machine.   | String   |

## Configure the Set VM CD/DVD to ISO Image Activity

To configure the Set VM CD/DVD to ISO Image Activity, follow these steps:

1.  From the **Activities** pane, drag a **Set VM CD/DVD to ISO Image** activity to the active runbook.

2.  Double-click the **Set VM CD/DVD to ISO Image** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
