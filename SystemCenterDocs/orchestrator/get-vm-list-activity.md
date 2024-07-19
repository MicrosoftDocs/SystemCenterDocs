---
title: Get VM List Activity
description: The Get VM List activity is used in a runbook to retrieve the virtual hardware information about a virtual machine in the VMware vSphere inventory.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 043ce1cb-31d6-47c7-991f-9278b01b0113
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 07/12/2024
---

# Get VM List Activity

The Get VM List activity is used in a runbook to retrieve the virtual hardware information about a virtual machine in the VMware vSphere inventory. This allows the runbook to retrieve the information of the virtual machine and populate it into a CMDB.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Get VM List Activity Required Properties

No required properties are provided for this activity.

### Get VM List Activity Optional Properties

No optional properties are provided for this activity.

### Get VM List Activity Filters

| Name   | Description   | Value Type | Relations   |
|:---|:---|:---|:---|
| Datacenter   | The datacenter hosting the VMs.   | String   | Equals   |
| Host/Cluster | The vSphere Host hosting the VMs. | String   | Equals   |
| ID   | The identifier of the VM.   | String   | Equals, Does not equal, Contains, Does not contain, Matches pattern, Does not match pattern, Starts with, Ends with. |
| VM Name   | The name of the VM.   | String   | Equals, Does not equal, Contains, Does not contain, Matches pattern, Does not match pattern, Starts with, Ends with. |
| VM path   | The full path of the VM.   | String   | Equals, Does not equal, Contains, Does not contain, Matches pattern, Does not match pattern, Starts with, Ends with. |

### Get VM List Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| ID   | The identifier of the VM.   | String   |
| VM Count | The number of VMs returned.   | String   |
| VM Name  | The name of the VM.   | String   |
| VM Path  | The full path of the VM on the vCenter server. | String   |

## Configure the Get VM List Activity

The following procedure describes the steps required to configure a Get VM List activity.

1. From the **Activities** pane, drag a **Get VM List** activity to the active runbook.

2. Double-click the **Get VM List** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Properties** tab as follows:

    1. In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.

4. On the **Filters** tab, select **Add** to add the filters required to restrict the published data.

5. Select **Finish**.
