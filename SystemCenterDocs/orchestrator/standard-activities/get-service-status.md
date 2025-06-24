---
title: Get Service Status
description: This article describes about the Get Service Status activity and its use to check the status of a service on any computer.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 212191ed-8156-45f1-bb09-0ccda3823d16
caps.latest.revision: 14
author: jyothisuri
ms.author: jsuri
---
# Get Service Status

The Get Service Status activity will check the status of a service on any computer. Use the Get Service Status to check the status of service before performing another action. For example, if you have an SQL Server backup runbook that requires that SQL Server is stopped before performing the backup, you can check the status and then stop the service using the [Start/Stop Service](start-stop-service.md) activity.  

## Configure the Get Service Status Activity

 Before you configure the Get Service Status activity, you need to determine the following:  

- The computer where the service is located  

- The name of the service  

Use the following information to configure the Get Service Status activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Type the name of the computer where the service that you're checking is located. You can also use the ellipsis **(...)** button to browse for the computer. The runbook server that runs this runbook must have the appropriate rights to monitor the services on that computer.|  
|**Service**|Type the name of the service that you're checking. You can also browse for the service using the ellipsis **(...)** button.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Service display name|The name of the service as it appears in the Windows Services control panel utility.|  
|Service real name|The name of the ran file that the service is running.|  
|Service status|The current status of the service.|  
|Service computer|The name of the computer where the service is located.|
