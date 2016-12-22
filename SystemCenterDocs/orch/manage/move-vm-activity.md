---
title: Move VM Activity
description: The Move VM activity is used in a runbook to move the virtual disk to a specific location, and can also associate the virtual machine with a different host.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27d7a05d-731c-4f03-bc34-c38a4938ae74
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Move VM Activity
================

Applies To: System Center 2016 - Orchestrator

The Move VM activity is used in a runbook to move the virtual disk to a specific location, and can also associate the virtual machine with a different host. This allows the runbook to move virtual machines from one host to another. When a virtual machine is moved, the disk files are moved and the host association is changed. To change the host association without moving the disk files, use the Migrate VM activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Move VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
| Destination Datastore   | The name of the data store that the moved virtual machine will use. If you leave this field blank, the current data store is used.   | String   | Yes   |
|:---|:---|:---|:---|
| Destination Host System   | The path of the destination host system.   | String   | Yes   |
| Destination Resource Pool | The path of the destination resource pool that the moved virtual machine will use. If you leave this field blank:<br> The current host is used if the resource pool is not specified.<br> If the resource pool is specified, and the target pool represents a stand-alone host, the stand-alone host is used.<br> If the resource pool is specified, and the target pool represents a DRS-enabled cluster, a host selected by DRS is used. You cannot specify a target pool that represents a cluster where DRS is not enabled. | String   | Yes   |
| VM Path   | The path to the virtual machine to be moved.   | String   | Yes   |

### Move VM Activity Optional Properties

|   |
|--------------------------------------------------------|
| No optional properties are provided for this activity. |

### Move VM Activity Published Data

| Name   | Description   | Value Type |
| Destination Datastore   | The name of the datastore that the moved virtual machine will use. | String   |
|:---|:---|:---|
| Destination Host System   | The path of the destination host system.   | String   |
| Destination Resource Pool | The path of the destination resource pool.   | String   |
| VM Path   | The path to the virtual machine that was moved.   | String   |

Configuring the Move VM Activity
--------------------------------

The following procedure describes the steps required to configure a Move VM activity.

#### To configure the Move VM Activity

1.  From the **Activities** pane, drag a **Move VM** activity to the active runbook.

2.  Double-click the **Move VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


