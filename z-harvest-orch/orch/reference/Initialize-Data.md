---
title: Initialize Data
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1cae147-b286-421d-b344-c73216ea9977
author:bwren
manager:cfreemanwa
---
# Initialize Data
The Initialize Data activity is a starting point for runbooks that require parameters from an Invoke Runbook activity. The Initialize Data activity is invoked by an [Invoke Runbook](../../orch/reference/Invoke-Runbook.md) activity. You can use the Initialize Data activity to launch generic runbooks that only perform specific actions. For example, use the Initialize Data activity to specify the files to back up in a runbook that performs backup operations. To return data to the invoking runbook, end the runbook's workflow with a [Return Data](../../orch/reference/Return-Data.md) activity.  
  
## Configuring the Initialize Data activity  
Before you configure the Initialize Data activity, you need to know the parameters that you want to use within your runbook.  
  
Use the following information to configure the Initialize Data activity.  
  
### Published Data  
Each parameter that you have configured is available as published data to the other activities in the runbook while the runbook is running. To pass data back to the invoking runbook, use the [Return Data](../../orch/reference/Return-Data.md) activity.  
  
## See Also  
[Invoke Runbook](../../orch/reference/Invoke-Runbook.md)  
[Return Data](../../orch/reference/Return-Data.md)  
  
