---
title: "Initialize Data | Microsoft Docs"
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
ms.assetid: c1cae147-b286-421d-b344-c73216ea9977
caps.latest.revision: 13
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Initialize Data

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The Initialize Data activity is a starting point for runbooks that require parameters from an Invoke Runbook activity. The Initialize Data activity is invoked by an [Invoke Runbook](invoke-runbook.md) activity. You can use the Initialize Data activity to launch generic runbooks that only perform specific actions. For example, use the Initialize Data activity to specify the files to back up in a runbook that performs backup operations. To return data to the invoking runbook, end the runbook’s workflow with a [Return Data](return-data.md) activity.  

## Configuring the Initialize Data activity  
 Before you configure the Initialize Data activity, you need to know the parameters that you want to use within your runbook.  

 Use the following information to configure the Initialize Data activity.  

### Published Data  
 Each parameter that you have configured is available as published data to the other activities in the runbook while the runbook is running. To pass data back to the invoking runbook, use the [Return Data](return-data.md) activity.  

## See Also  
 [Invoke Runbook](invoke-runbook.md)   
 [Return Data](return-data.md)
