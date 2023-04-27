---
title: Get Disk Space Status
description: This article describes the Get Disk Space Status activity.
ms.custom: UpdateFrequency3
ms.date: 05/27/2023
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e092f55e-b9bd-4e78-8609-1bb5676b7dce
caps.latest.revision: 13
author: "jyothisuri"
ms.author: "jsuri"
manager: mkluck
---
# Get Disk Space Status

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The Get Disk Space Status activity will retrieve the current amount of available disk space on a UNC path or local disk drive that you specify. This activity can be used to check the space of a destination folder before transferring files to that location.  

## Configuring the Get Disk Space Status Activity  
 Before you configure the Get Disk Space Status activity, you need to determine the UNC path or local drive that you want to check.  

 Use the following information to configure the Get Disk Space Status activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer that you're checking. You can also use the ellipsis **(...)** button to browse for the computer.|  
|**Drive**|Enter the drive path you want to check. To specify a local drive path, include the colon and backslash. For example, to specify the Local Disk (C:), enter `"C:\"`. If you specify a local drive path, the runbook server that runs the runbook will check its local drive. The runbook server that runs this runbook must have the appropriate rights to check the process on the computer on which you're checking the disk space status.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Drive|The drive that's being monitored.|  
|Percentage of Space available|The percentage of the entire drive capacity that's available.|  
|MB available|The number of megabytes available on the drive.|  
|GB available|The number of gigabytes available on the drive.|