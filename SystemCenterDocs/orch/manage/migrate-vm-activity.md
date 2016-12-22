---
title: Migrate VM Activity
description: The Migrate VM activity is used in a runbook to migrate a virtual machine in any state (powered on, powered off, or suspended) to another computer.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 748c58c3-6ef0-4249-b6bc-51f756d89f61
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Migrate VM Activity
===================

Applies To: System Center 2016 - Orchestrator

The Migrate VM activity is used in a runbook to migrate a virtual machine in any state (powered on, powered off, or suspended) to another computer. This allows the runbook to change the host system association when the host computer is upgraded. When a virtual machine is migrated only the host computer association is changed, the disk files are not moved. To move the disk files and change the host association, the Move VM activity must be used.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Migrate VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
| Destination Host System   | The path to the destination host system.   | String   | Yes   |
|:---|:---|:---|:---|
| Destination Resource Pool | The path to the destination resource pool that the migrated virtual machine will use. | String   | Yes   |
| Move Priority   | The priority level for the migration operation   | String   | Yes   |
| VM Path   | The path to the virtual machine to be migrated   | String   | Yes   |

### Migrate VM Activity Optional Properties

|   |
|--------------------------------------------------------|
| No optional properties are provided for this activity. |

### Migrate VM Activity Published Data

| Name   | Description   | Value Type |
| Destination Host System   | The path to the destination host system   | String   |
|:---|:---|:---|
| Destination Resource Pool | The path to the destination resource pool.   | String   |
| Move Priority   | The priority level assigned to the migration.   | String   |
| VM Path   | The path to the virtual machine that was migrated. | String   |

Configuring the Migrate VM Activity
-----------------------------------

The following procedure describes the steps required to configure a Migrate VM activity.

#### To configure the Migrate VM Activity

1.  From the **Activities** pane, drag a **Migrate VM** activity to the active runbook.

2.  Double-click the **Migrate VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


