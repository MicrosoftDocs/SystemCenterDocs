---
title: End Process
description: This article describes the End Process activity that ends processes that are running on the runbook server or on a remote computer.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/21/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 349554ed-af74-42fd-b061-bb75e0a3bd0f
caps.latest.revision: 18
author: Jeronika-MS
ms.author: v-gajeronika
---
# End Process

The End Process activity ends processes that are running on the runbook server or on a remote computer. The End Process activity can be used to shut down an application that isn't responding. The activity returns **success** if the named process is successfully ended or if the name process isn't running. This activity uses a satellite license.  

## Configure the End Process Activity

 Before you configure the End Process activity, you need to determine the following:  

- Name or ID of the process  

- The computer on which it's running  

Use the following information to configure the End Process activity:  

## Details tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the computer where this process is running. Enter `localhost` to specify the runbook server where the runbook is being processed. You can also use the ellipsis button **(...)** to browse for the computer.|  
|**Process**|Enter the name or process ID of the process that you're ending. You can also use the ellipsis button **(...)** to browse for the process. Browsing is only available if you've specified a valid **Computer**.|  
|**End all instances**|Select to end all processes that match the Process that you've specified when multiples are found.|  
|**Fail if there is more than one instance**|Select to cause the end process to fail if it finds more than one process matching the name you specified.|  
|**Terminate in**|Enter the number of seconds to wait for the process to be shut down gracefully before it's shut down forcefully.|  

## Published data  

 The following table lists the published data items:  

|Item|Description|  
|----------|-----------------|  
|Number of instances|The number of processes that matched the **Process** you specified.|  
|Process ID|The process ID of each of the processes that matched the **Process** you specified.|
