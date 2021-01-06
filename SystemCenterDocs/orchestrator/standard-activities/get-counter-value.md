---
title: "Get Counter Value | Microsoft Docs"
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
ms.assetid: fe935ce1-871b-451b-8ce7-e2d3084463d6
caps.latest.revision: 13
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Get Counter Value

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The Get Counter Value activity retrieves the value of a counter and returns it as a published data item. Wherever you need to use the value of a counter, use the published data that is published by the Get Counter Value to retrieve that value.  

## Configuring the Get Counter Value Activity  
 Before you configure the Get Counter Value activity, you need to determine which counter you will retrieve.  

> [!WARNING]
>  Before you can use this activity, you must configure a Counter. To modify a counter, use the [Modify Counter](modify-counter.md) activity.

 Use the following information to configure the Get Counter Value activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|Counter|Click the ellipsis **(...)** button to select the **Counter** that you are retrieving.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Counter Value|The value of the counter.|
