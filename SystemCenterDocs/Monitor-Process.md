---
title: Monitor Process
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c97c68d-f3f5-4840-86b5-43501d575edf
---
# Monitor Process
The Monitor Process activity invokes runbooks when a process has been started or stopped. A process is any executable file that is running. You can use the Monitor Process activity to monitor processes on any remote computer.

The Monitor Process activity can be used to create runbooks that take corrective actions when a process has been started but has not stopped. For example, if an application that has a tendency to stop responding and remain resident in memory even though it has completed, it can be shut down automatically by using a Monitor Process activity in a runbook with a [Get Process Status](./Get-Process-Status.md) activity to retrieve the status of the process and an [End Process](./End-Process.md) activity to shut it down.

## Configuring the Monitor Process Activity
Before you configure the Monitor Process activity, you will need to determine the following:

-   Which computer will run the process that you are monitoring

-   Which process you want to monitor

-   Whether the runbook will be ran when the process is started or stopped

Use the following information to configure the Monitor Process activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer where the process that you are monitoring is located. You can also browse for the computer using the ellipsis **\(...\)** button. The runbook server that runs this runbook must have the appropriate rights to monitor the process on that computer.|
|**Process**|Type the name of the process that you are monitoring. You can also browse for the process using the ellipsis **\(...\)** button.|
|**Process is started**|Select to invoke the Monitor Process activity when the selected process has been started.|
|**Process is stopped**|Select to invoke the Monitor Process activity when the last running instance of the selected process has been stopped.|
|**Test frequency**|Select the amount of time to wait between each time that the Monitor Process activity checks the status of the process.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Computer|The name of the computer where the process is located.|
|Process name|The name of the process ran.|
|Number of instances for the process|The number of running occurrences of the process.|
|Test interval|The number of seconds between each check of the process status.|
|Invokes on process start|Determines whether the runbook will be invoked if the process is started.|
|Invokes on process end|Determines whether the runbook will be invoked if the process is stopped.|


