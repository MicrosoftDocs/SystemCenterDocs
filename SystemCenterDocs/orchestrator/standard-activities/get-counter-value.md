---
title: Get Counter Value
description: This article describes the functionality of Get Counter Value activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: fe935ce1-871b-451b-8ce7-e2d3084463d6
caps.latest.revision: 13
author: jyothisuri
ms.author: jsuri
---
# Get Counter Value

The Get Counter Value activity retrieves the value of a counter and returns it as a published data item. Wherever you need to use the value of a counter, use the published data that is published by the Get Counter Value to retrieve that value.  

## Configure the Get Counter Value Activity

 Before you configure the Get Counter Value activity, you need to determine which counter you'll retrieve.  

> [!WARNING]
> Before you can use this activity, you must configure a Counter. To modify a counter, use the [Modify Counter](modify-counter.md) activity.

 Use the following information to configure the Get Counter Value activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|Counter|Select the ellipsis **(...)** to select the **Counter** that you're retrieving.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Counter Value|The value of the counter.|
