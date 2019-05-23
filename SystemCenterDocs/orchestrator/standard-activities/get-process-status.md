---
title: "Get Process Status | Microsoft Docs"
ms.custom: ""
ms.date: "2016-05-13"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: 58173cdc-97ea-4ecf-a7b8-4e48c30fea5b
caps.latest.revision: 18
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Get Process Status
The Get Process Status activity checks the status of a running process on any computer. Use the Get Process Status activity to check the status of a process before performing another action. For example, you can check that a process that was detected by the [Monitor Process](monitor-process.md) activity is still running before shutting it down with the [End Process](end-process.md) activity.  

> [!IMPORTANT]
>  The Get Process Status activity returns a status of **failed** if the named process is not running. If the activity returns **failed**, the overall status of the runbook is set to **warning** or **failed**, depending on the number of activities in the runbook.  

## Configuring the Get Process Status Activity  
 Before you configure the Get Process Status activity, you need to determine the following:  

- The computer where the process is located.  

- The file name that will run the process.  

Use the following information to configure the Get Process Status activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Type the name of the computer where the process that you are checking is located. You can also browse for the computer using the ellipsis **(...)** button. The runbook server that runs this runbook must have the appropriate rights to check the process on that computer.|  
|**Process**|Type the name of the process that you are checking. You can also browse for the process using the ellipsis **(...)** button.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer|The name of the computer where the process is located.|  
|Process name|The name of the process ran.|  
|Process ID|The ID of the process.|  
|Number of instances for the process|The number of running occurrences of the process.|
