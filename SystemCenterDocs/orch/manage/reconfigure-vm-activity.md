---
title: Reconfigure VM Activity
description: The Reconfigure VM activity is used in a runbook to change the hardware settings of a virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9917c4f-376f-4a60-88b5-c141e4200c9f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Reconfigure VM Activity

Applies To: System Center 2016 - Orchestrator

The Reconfigure VM activity is used in a runbook to change the hardware settings of a virtual machine. This allows the runbook to increase the number of CPUs and Memory to increase the availability of the application running in the guest operating system.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Reconfigure VM Activity Required Properties

| Element | Description   | Valid Values | Look up |
| Notes   | The notes associated with the virtual machine.   | String   | No   |
|:---|:---|:---|:---|
| VM Path | The path of the virtual machine to be reconfigured. | String   | Yes   |

### Reconfigure VM Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
| After Power On Script   | Indicates whether a script will be run after the virtual machine is powered on.   | String   | Yes   |
|:---|:---|:---|:---|
| After Resume Script   | Indicates whether a script will be run after the virtual machine is resumed from standby. | String   | Yes   |
| Before Guest Shutdown Script   | Indicates whether a script will be run before the virtual machine is shut down.   | String   | Yes   |
| Before Guest Standby Script   | Indicates whether a script will be run before the virtual machine is put into standby.   | String   | Yes   |
| CPUs   | The number of CPUs assigned to the virtual machine   | Integer   | Yes   |
| CPU Limit Specified   | Must be true if a CPU Limit has been specified.   | Boolean   | Yes   |
| CPU Reservation (MHz)   | The amount of CPU resources that are reserved for the VM, in megahertz.   | Integer   | No   |
| CPU Reservation Specified   | Must be true if CPU Reservation is specified.   | Boolean   | Yes   |
| CPU Shares Level   | The relative CPU priority given to this VM. Custom, low, normal, high.   | String   | Yes   |
| CPU Limit(-1 means unlimited)   | The CPU utilization limit for the VM within the resource pool.   | Integer   | No   |
| Custom CPU Shares Level   | The CPU Shares Level property must be set to custom for this property to be processed.   | Integer   | No   |
| Custom Memory Shares Level   | The Memory Shares Level property must be set to custom for this property to be processed. | Integer   | No   |
| Memory   | The amount of memory assigned to the virtual machine   | Integer   | No   |
| Memory Limit Specified   | Must be true if a Memory Limit has been specified.   | Boolean   | Yes   |
| Memory Limit(-1 means unlimited) | The memory utilization limit for the VM within the resource pool.   | Integer   | No   |
| Memory Reservation (MB)   | The amount of memory resources that are reserved for the VM, in megabytes.   | Integer   | No   |
| Memory Reservation Specified   | Must be true if Memory Reservation is specified.   | Boolean   | Yes   |
| Memory Shares Level   | The relative Memory priority given to this VM. Custom, low, normal, high.   | String   | Yes   |
| Power Off Type   | The action that will occur when the virtual machine is instructed to power off.   | String   | Yes   |
| Reset Type   | The action that will occur when the virtual machine is instructed to reset.   | String   | Yes   |
| Suspend Type   | The action that will occur when the virtual machine is instructed to suspend.   | String   | Yes   |
| VM Name   | The new name of the virtual machine.   | String   | No   |

### Reconfigure VM Activity Published Data

| Name   | Description   | Value Type |
| After Power On Script   | Indicates whether a script will be run after the virtual machine is powered on.   | String   |
|:---|:---|:---|
| After Resume Script   | Indicates whether a script will be run after the virtual machine is resumed from standby. | String   |
| Before Guest Shutdown Script | Indicates whether a script will be run before the virtual machine is shut down.   | String   |
| Before Guest Standby Script  | Indicates whether a script will be run before the virtual machine is put into standby.   | String   |
| CPUs   | The number of CPUs assigned to the virtual machine.   | Integer   |
| CPU Limit Specified   | Must be true if a CPU Limit has been specified.   | Boolean   |
| CPU Reservation (MHz)   | The amount of CPU resources that are reserved for the VM, in megahertz.   | Integer   |
| CPU Reservation Specified   | Must be true if CPU Reservation is specified.   | Boolean   |
| Custom CPU Shares Level   | The relative CPU priority given to this VM. Custom, low, normal, high.   | String   |
| CPU Limit   | The CPU utilization limit for the VM within the resource pool.   | Integer   |
| Custom CPU Shares Level   | The CPU Shares Level property must be set to custom for this property to be processed.   | Integer   |
| Custom Memory Shares Level   | The Memory Shares Level property must be set to custom for this property to be processed. | Integer   |
| Memory   | The amount of memory assigned to the virtual machine.   | Integer   |
| Memory Limit Specified   | Must be true if a Memory Limit has been specified.   | Boolean   |
| Memory Limit   | The memory utilization limit for the VM within the resource pool.   | Integer   |
| Memory Reservation (MB)   | The amount of memory resources that are reserved for the VM, in megabytes.   | Integer   |
| Memory Reservation Specified | Must be true if Memory Reservation is specified.   | Boolean   |
| Memory Shares Level   | The relative Memory priority given to this VM. Custom, low, normal, high.   | String   |
| Notes   | The notes associated with the virtual machine.   | String   |
| Power Off Type   | The action that occurs when the virtual machine is instructed to power off.   | String   |
| Reset Type   | The action that occurs when the virtual machine is instructed to reset.   | String   |
| Suspend Type   | The action that occurs when the virtual machine is instructed to suspend.   | String   |
| VM Name   | The new name of the virtual machine.   | String   |
| VM Path   | The path to the virtual machine to be reconfigured.   | String   |

## Configuring the Reconfigure VM Activity

The following procedure describes the steps required to configure a Reconfigure VM activity.

#### To configure the Reconfigure VM Activity

1.  From the **Activities** pane, drag a **Reconfigure VM** activity to the active runbook.

2.  Double-click the **Reconfigure VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


