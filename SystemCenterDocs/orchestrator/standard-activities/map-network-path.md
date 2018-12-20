---
title: "Map Network Path | Microsoft Docs"
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
ms.assetid: 8954602d-8f80-4a5d-8e69-fd8148122ac6
caps.latest.revision: 14
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Map Network Path
The Map Network Path activity enables you to map a network path using a UNC path.  
  
## Configuring the Map Network Path Activity  
 Before you configure the Map Network Path activity, you need to determine the following:  
  
-   The UNC path you want to map.  
  
-   The user account and password you need to log into that path; if required.  
  
 Use the following information to configure the Map Network Path activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Network path**|Type the network path that you want to connect to in UNC format (\\\servername\foldername), or click the ellipsis button **(...)** and browse for it.<br /><br /> Verify that the network path that you want to map does not already exist.|  
|**User account**|Type the user account that you need to access the network path.|  
|**Password**|Type the password that you need to access the network path.|  
  
### Published Data  
 The following table lists the published data items.  
  
|Item|Description|  
|----------|-----------------|  
|Network path|The network path that you are mapping.|  
|User account|The user account that you used to access the network path.|