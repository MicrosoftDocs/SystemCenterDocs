---
title: "Disconnect Network Path | Microsoft Docs"
ms.custom: ""
ms.date: "2016-05-13"
ms.prod: "system-center-2012"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "orchestrator"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: d697232c-7604-4e8e-bde9-1d8e55a1c220
caps.latest.revision: 11
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Disconnect Network Path
The Disconnect Network Path activity allows you to disconnect a network path. You can disconnect network paths you mapped using the [Map Network Path](map-network-path.md) activity or using another method.  
  
## Configuring the Disconnect Network Path Activity  
 Before you configure the Disconnect Network Path activity, you need to determine the network path you want to disconnect.  
  
> [!NOTE]
>  You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  
  
 Use the following information to configure the Disconnect Network Path activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Network path**|Type the name of the network path that you want to disconnect, or click the ellipsis button **(...)** and browse for it.|  
  
### Published Data  
 The following table lists the published data items.  
  
|Item|Description|  
|----------|-----------------|  
|Network path|The network path you are disconnecting.|