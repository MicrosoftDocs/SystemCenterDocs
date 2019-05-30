---
title: "Query WMI | Microsoft Docs"
ms.custom: ""
ms.date: "2016-05-13"
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
ms.assetid: 979b6b2d-8aba-48e3-a42a-8553cdd08559
caps.latest.revision: 19
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Query WMI
The Query WMI activity will send a WMI query to a system that you specify and return the results. This activity also can be used to check statistics on a remote server to create audit trails that can be reviewed later.  

## Configuring the Query WMI Activity  
 Before you configure the Query WMI activity, you need to determine the following:  

- The computer you are querying.  

- The WMI query statement you want to run.  

Use the following information to configure the Query WMI activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Type the name of the computer that you are running the WMI query against. You can also use the ellipsis **(...)** button to browse for the computer.|  
|**Namespace**|Type the name of the WMI namespace that you want to query.|  
|**WMI query**|Type the WMI query that will be used to query the **Computer**. For more information about Windows Management Instrumentation, see [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=221343) (http://go.microsoft.com/fwlink/?LinkId=221343).|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer where the WMI query is performed|The name of the computer where the WMI query was ran.|  
|WMI Query|The WMI query that was sent to the computer.|  
|WMI Query Result as a string|The result of the WMI query.|  
|WMI Namespace|The WMI namespace that you queried.|
