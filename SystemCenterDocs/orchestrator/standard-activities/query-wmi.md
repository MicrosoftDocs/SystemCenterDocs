---
title: Query WMI
description: This article describes the Query WMI activity that will send a WMI query to a system that you specify and return the results.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/21/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 979b6b2d-8aba-48e3-a42a-8553cdd08559
caps.latest.revision: 19
author: jyothisuri
ms.author: jsuri
---
# Query WMI

This article describes the Query WMI activity that will send a WMI query to a system that you specify and return the results. This activity can also be used to check statistics on a remote server to create audit trails that can be reviewed later.  

## Configure the Query WMI Activity

 Before you configure the Query WMI activity, you need to determine the following:  

- The computer you are querying.  

- The WMI query statement you want to run.  

Use the following information to configure the Query WMI activity:  

### Details Tab  

|Settings|Configuration instructions|  
|--------------|--------------------------------|  
|**Computer**|Type the name of the computer that you are running the WMI query against. You can also use the ellipsis **(...)** button to browse for the computer.|  
|**Namespace**|Type the name of the WMI namespace that you want to query.|  
|**WMI query**|Type the WMI query that will be used to query the **Computer**. For more information about Windows Management Instrumentation, see [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page).|  

### Published Data

 The following table lists the published data items:  

|Item|Description|  
|----------|-----------------|  
|Computer where the WMI query is performed|The name of the computer where the WMI query was ran.|  
|WMI Query|The WMI query that was sent to the computer.|  
|WMI Query Result as a string|The result of the WMI query.|  
|WMI Namespace|The WMI namespace that you queried.|
