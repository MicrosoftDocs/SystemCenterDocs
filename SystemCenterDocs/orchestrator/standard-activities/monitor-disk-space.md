---
title: "Monitor Disk Space | Microsoft Docs"
ms.custom: ""
ms.date: "05/13/2016"
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
ms.assetid: a88637be-d698-4cd6-8224-219394e64518
caps.latest.revision: 12
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Monitor Disk Space

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The Monitor Disk Space activity will invoke a runbook when the disk space on a computer passes a critical threshold. You can monitor multiple drives on different computers with a single Monitor Disk Space activity. The Monitor Disk Space activity can be used to invoke runbooks that will automatically backup and purge files on a hard drive that is running out of space  

## Configuring the Monitor Disk Space Activity  
 Before you configure the Monitor Disk Space activity, you need to determine the following:  

- The drives that you want to monitor  

- The computer where those drives are located  

The runbook server that runs this runbook must have the appropriate rights to check the process on the computer that you are monitoring.  

Use the following information to configure the Monitor Disk Space activity.  

### Test frequency example: Monitor Disk Space activity is set to test every 30 seconds  

|Time|All Disks are Passed Threshold?|Result|  
|----------|-------------------------------------|------------|  
|30s|No|Do not trigger runbook|  
|60s|Yes|Trigger runbook|  
|90s|Yes|Do not trigger runbook|  
|120s|No|Do not trigger runbook|  
|150s|Yes|Trigger runbook|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer|The name of the computer where the drive is being monitored.|  
|Drive|The drive that is being monitored.|  
|Percentage of Space available|The percentage of the entire drive capacity that is available.|  
|MB available|The number of megabytes available on the drive.|  
|GB available|The number of gigabytes available on the drive.|  
|Test interval|The number of seconds between each test of the disk space.|
