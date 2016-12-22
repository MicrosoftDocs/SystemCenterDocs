---
title: Get VM Properties Activity
description: The Get VM Properties activity is used in a runbook retrieve the virtual hardware information about a virtual machine in the VMware vSphere inventory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c10df30c-2768-4407-9599-77eb0e1c7d42
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get VM Properties Activity
==========================

Applies To: System Center 2016 - Orchestrator

The Get VM Properties activity is used in a runbook retrieve the virtual hardware information about a virtual machine in the VMware vSphere inventory. This, for example, enables the runbook to retrieve the information of the virtual machine and populate it into a CMDB.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Get VM Properties Activity Required Properties

| Name   | Description   | Valid Values | Look up |
| VM Path | The path of the virtual machine in the vSphere hierarchy. | String   | Yes   |
|:---|:---|:---|:---|

### Get VM Properties Activity Optional Properties

|   |
|-------------------------------------------------------|
| No optional properties are provided for this activity |

### Get VM Properties Activity Published Data

| Name   | Description   | Value Type |
| Address Type | The address type of the Network Interface MAC address   | String   |
|:---|:---|:---|
| Hard Disks   | A list of device IDs for the virtual disks connected to the VM. | Integer   |
| Host name   | The DNS host name assigned to the guest VM.   | String   |
| MAC Address  | The MAC address of the VMs primary network interface.   | String   |
| Memory MB   | The memory allocated to the VM in megabytes.   | String   |
| VM Path   | The path of the virtual machine in the vSphere hierarchy.   | String   |

Configuring the Get VM Properties Activity
------------------------------------------

The following procedure describes the steps required to configure a Get VM Properties activity.

#### To configure the Get VM Properties Activity

1.  From the **Activities** pane, drag a **Get VM Properties** activity to the active runbook.

2.  Double-click the **Get VM Properties** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


