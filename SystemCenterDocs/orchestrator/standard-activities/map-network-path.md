---
title: Map Network Path
description: This articles describes the functionality of Map Network Path activity.
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
ms.assetid: 8954602d-8f80-4a5d-8e69-fd8148122ac6
caps.latest.revision: 14
author: "jyothisuri"
ms.author: "jsuri"
manager: "evansma"
---
# Map Network Path

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The Map Network Path activity enables you to map a network path using a UNC path.  

## Configuring the Map Network Path Activity  
 Before you configure the Map Network Path activity, you need to determine the following:  

- The UNC path you want to map.  

- The user account and password you need to sign into that path, if required.  

Use the following information to configure the Map Network Path activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Network path**|Enter the network path that you want to connect to in UNC format (\\\servername\foldername), or select the ellipsis button **(...)** and browse for it.<br /><br /> Verify that the network path that you want to map does not already exist.|  
|**User account**|Enter the user account that you need to access the network path.|  
|**Password**|Enter the password that you need to access the network path.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Network path|The network path that you're mapping.|  
|User account|The user account that you used to access the network path.|