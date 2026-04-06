---
title: Monitor Disk Space
description: This article describes the Monitor Disk Space activity that will invoke a runbook when the disk space on a computer passes a critical threshold.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: a88637be-d698-4cd6-8224-219394e64518
caps.latest.revision: 12
author: Jeronika-MS
ms.author: v-gajeronika
---
# Monitor Disk Space

The Monitor Disk Space activity will invoke a runbook when the disk space on a computer passes a critical threshold. You can monitor multiple drives on different computers with a single Monitor Disk Space activity. The Monitor Disk Space activity can be used to invoke runbooks that will automatically backup and purge files on a hard drive that is running out of space  

## Configure the Monitor Disk Space Activity

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
