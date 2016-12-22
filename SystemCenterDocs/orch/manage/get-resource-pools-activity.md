---
title: Get Resource Pools Activity
description: The Get Resource Pools activity is used in a runbook to retrieve a list of all the resource pools in managed by the VMware vSphere system.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 662fa33f-d507-4721-9369-b5c2ad518731
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get Resource Pools Activity
===========================

Applies To: System Center 2016 - Orchestrator

The Get Resource Pools activity is used in a runbook to retrieve a list of all the resource pools in managed by the VMware vSphere system. This allows the runbook to retrieve the resources pools before using the Get Resource Pool Runtime Info Activity.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Get Resource Pools Activity Required Properties

|   |
|--------------------------------------------------------|
| No required properties are provided for this activity. |

### Get Resource Pools Activity Optional Properties

|   |
|--------------------------------------------------------|
| No optional properties are provided for this activity. |

### Get Resource Pools Activity Published Data

| Name   | Description   | Value Type |
| Resource Pool | A list of resource pool paths within the vCenter server. | String   |
|:---|:---|:---|

Configuring the Get Resource Pools Activity
-------------------------------------------

The following procedure describes the steps required to configure a Get Resource Pools activity.

#### To configure the Get Resource Pools Activity

1.  From the **Activities** pane, drag a **Get Resource Pools** activity to the active runbook.

2.  Double-click the **Get Resource Pools** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.

4.  Click **Finish**.


