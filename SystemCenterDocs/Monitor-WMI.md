---
title: Monitor WMI
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d825cef7-e68a-4387-829e-c3602bed2b6a
---
# Monitor WMI
The Monitor WMI activity invokes a runbook when a WMI event is received as a result of the WMI event query that you specify.  You can check for changes in devices that are attached to the server and invoke runbooks that take corrective action when errors occur.

## Configuring the Monitor WMI Activity
Before you configure the Monitor WMI activity, you need to determine the following:

-   The computer that you are monitoring

-   The WMI event query that you want to run

> [!WARNING]
> A WMI event query differs from a standard WMI query.

Use the following information to configure the Monitor WMI activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer that you are monitoring for new WMI events. You can also use the ellipsis **\(...\)** button to browse for the computer.|
|**Namespace**|Type the name of the WMI namespace that you want to query.|
|**WMI query**|Type the WMI event query that will be used to query the computer that you specified in the **Computer** box.|

### Syntax Examples
Here is the syntax of a simple notification query: `SELECT * FROM [EventClass] WITHIN [interval] WHERE TargetInstance ISA [object]`

When you submit this WMI query, you are submitting a job to be notified of all occurrences of the event represented by \[EventClass\]. The WITHIN clause denotes how the test is performed, which is at an interval of seconds denoted by \[interval\]. The WHERE clause is used to narrow down your query and can include activities, properties of embedded activities and condition statements.

**Monitor for the Addition of a Modem**: The following query submits a notification job to monitor for the addition of a modem and will cause the WMI event to invoke if a modem is added. The test is performed at an interval of every 10 seconds. `SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "Win32_POTSModem"`

**Monitor for the Deletion of a Modem:** The following query submits a notification job to monitor for the deletion of a modem and will cause the WMI event to invoke if a modem is deleted. The test is performed at an interval of every 50 seconds. `SELECT * FROM __InstanceDeletionEvent WITHIN 50 WHERE TargetInstance ISA "Win32_POTSModem"`

**Monitor for the Modification of a Display Configuration**: The following query submits a notification job to monitor for the modification of a display configuration and will cause the WMI event to invoke if the display frequency is greater than 70. The test is performed at an interval of every 20 seconds. `SELECT * FROM __InstanceModificationEvent WITHIN 20 WHERE TargetInstance ISA "Win32_DisplayConfiguration" AND TargetInstance.DisplayFrequency > 70`

**Monitor for a Modification in a Processor value**: The following query submits a notification job to monitor for a modification in a Processor value and will cause the WMI event to invoke if the CPU utilization is greater than 50. The test is performed at an interval of every 5 seconds. `SELECT * FROM __InstanceModificationEvent WITHIN 5 WHERE TargetInstance ISA "Win32_Processor" AND TargetInstance.LoadPercentage > 50`

> [!TIP]
> A query can be rejected by WMI if it is too complex or becomes resource\-intensive for evaluation.

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Computer where the WMI query is performed|The name of the computer where the WMI query was ran.|
|WMI Query|The WMI query that was sent to the computer.|
|WMI Query Result as a string|The result of the WMI query.|
|WMI Namespace|The WMI namespace that you queried.|


