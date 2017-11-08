---
title: Get Cluster Properties Activity
description: The Get Cluster Properties activity is used in a runbook to retrieve information about a virtual machine cluster in VMware vSphere.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6a413406-a44f-4f36-b3fc-1a8c066e0b8e
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# Get Cluster Properties Activity

The Get Cluster Properties activity is used in a runbook to retrieve information about a virtual machine cluster in VMware vSphere. This allows the runbook to obtain the information about a cluster before cloning or creating virtual machines on that cluster.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get Cluster Properties Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Cluster Path | The path to the virtual machine cluster whose properties are being retrieved | String   | Yes   |


## Get Cluster Properties Activity Optional Properties

No optional properties are provided for this activity.

## Get Cluster Properties Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Cluster Path   | The path of the virtual machine cluster.   | String   |
| Datastore Names   | The names of the datastores assigned to the cluster.   | String   |
| Effective CPU (MHz)   | The total CPU MHZ available for virtual machines.   | Integer   |
| Effective Memory (MB)   | The total memory available for virtual machines.   | Integer   |
| Number of CPU Cores   | The total number of CPU cores assigned to the virtual machine cluster.   | Integer   |
| Number of CPU Threads   | The total number of available CPU threads on the virtual machine cluster. | Integer   |
| Number of Effective Hosts | The total number of hosts available for hosting virtual machines.   | Integer   |
| Number of Hosts   | The total number of hosts in the virtual machine cluster.   | Integer   |
| Total CPU (MHz)   | The total CPU MHz available on the virtual machine cluster.   | Integer   |
| Total Memory (MB)   | The total memory available on the virtual machine cluster.   | Integer   |

## Configuring the Get Cluster Properties Activity

The following procedure describes the steps required to configure a Get Cluster Properties activity.

### To configure the Get Cluster Properties Activity

1.  From the **Activities** pane, drag a **Get Cluster Properties** activity to the active runbook.
2.  Double-click the **Get Cluster Properties** activity icon. The **Properties** dialog box opens.
3.  Configure the settings in the **Properties** tab as follows:
    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.<br>You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.
