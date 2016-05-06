---
title: Get Process Status
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58173cdc-97ea-4ecf-a7b8-4e48c30fea5b
---
# Get Process Status
The Get Process Status activity checks the status of a running process on any computer. Use the Get Process Status activity to check the status of a process before performing another action. For example, you can check that a process that was detected by the [Monitor Process](../Topic/Monitor-Process.md) activity is still running before shutting it down with the [End Process](../Topic/End-Process.md) activity.

> [!IMPORTANT]
> The Get Process Status activity returns a status of **failed** if the named process is not running. If the activity returns **failed**, the overall status of the runbook is set to **warning** or **failed**, depending on the number of activities in the runbook.

## Configuring the Get Process Status Activity
Before you configure the Get Process Status activity, you need to determine the following:

-   The computer where the process is located.

-   The file name that will run the process.

Use the following information to configure the Get Process Status activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer where the process that you are checking is located. You can also browse for the computer using the ellipsis **\(...\)** button. The runbook server that runs this runbook must have the appropriate rights to check the process on that computer.|
|**Process**|Type the name of the process that you are checking. You can also browse for the process using the ellipsis **\(...\)** button.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Computer|The name of the computer where the process is located.|
|Process name|The name of the process ran.|
|Process ID|The ID of the process.|
|Number of instances for the process|The number of running occurrences of the process.|

