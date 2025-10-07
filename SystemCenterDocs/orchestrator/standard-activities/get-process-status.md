---
title: Get Process Status
description: This article describes the functionality of Get Process Status activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 58173cdc-97ea-4ecf-a7b8-4e48c30fea5b
caps.latest.revision: 18
author: Jeronika-MS
ms.author: v-gajeronika
---
# Get Process Status

The Get Process Status activity checks the status of a running process on any computer. Use the Get Process Status activity to check the status of a process before performing another action. For example, you can check that a process that was detected by the [Monitor Process](monitor-process.md) activity is still running before shutting it down with the [End Process](end-process.md) activity.  

> [!IMPORTANT]
> The Get Process Status activity returns a status of **failed** if the named process is not running. If the activity returns **failed**, the overall status of the runbook is set to **warning** or **failed**, depending on the number of activities in the runbook.  

## Configure the Get Process Status Activity

 Before you configure the Get Process Status activity, you need to determine the following:  

- The computer where the process is located.  

- The file name that will run the process.  

Use the following information to configure the Get Process Status activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the process that you're checking is located. You can also browse for the computer using the ellipsis **(...)** button. The runbook server that runs this runbook must have the appropriate rights to check the process on that computer.|  
|**Process**|Enter the name of the process that you're checking. You can also browse for the process using the ellipsis **(...)** button.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer|The name of the computer where the process is located.|  
|Process name|The name of the process run.|  
|Process ID|The ID of the process.|  
|Number of instances for the process|The number of running occurrences of the process.|
