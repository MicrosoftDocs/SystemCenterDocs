---
title: Get VM List Activity
description: The Get VM List activity is used in a runbook retrieve the virtual hardware information about a virtual machine in the VMware vSphere inventory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 043ce1cb-31d6-47c7-991f-9278b01b0113
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get VM List Activity

Applies To: System Center 2016 - Orchestrator

The Get VM List activity is used in a runbook retrieve the virtual hardware information about a virtual machine in the VMware vSphere inventory. This allows the runbook to retrieve the information of the virtual machine and populate it into a CMDB.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Get VM List Activity Required Properties

|   |
|--------------------------------------------------------|
| No required properties are provided for this activity. |

### Get VM List Activity Optional Properties

|   |
|-------------------------------------------------------|
| No optional properties are provided for this activity |

### Get VM List Activity Filters

| Name   | Description   | Value Type | Relations   |
| Datacenter   | The datacenter hosting the VMs.   | String   | Equals   |
|:---|:---|:---|:---|
| Host/Cluster | The vSphere Host hosting the VMs. | String   | Equals   |
| ID   | The identifier of the VM.   | String   | Equals, Does not equal, Contains, Does not contain, Matches pattern, Does not match pattern, Starts with, Ends with. |
| VM Name   | The name of the VM.   | String   | Equals, Does not equal, Contains, Does not contain, Matches pattern, Does not match pattern, Starts with, Ends with. |
| VM path   | The full path of the VM.   | String   | Equals, Does not equal, Contains, Does not contain, Matches pattern, Does not match pattern, Starts with, Ends with. |

### Get VM List Activity Published Data

| Name   | Description   | Value Type |
| ID   | The identifier of the VM.   | String   |
|:---|:---|:---|
| VM Count | The number of VMs returned.   | String   |
| VM Name  | The name of the VM.   | String   |
| VM Path  | The full path of the VM on the vCenter server. | String   |

## Configuring the Get VM List Activity

The following procedure describes the steps required to configure a Get VM List activity.

#### To configure the Get VM List Activity

1.  From the **Activities** pane, drag a **Get VM List** activity to the active runbook.

2.  Double-click the **Get VM List** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.

4.  On the **Filters** tab, click **Add** to add the filters required to restrict the published data.

5.  Click **Finish**.


