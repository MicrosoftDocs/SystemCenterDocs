---
title: Disconnect Network Path
description: This article describes the Disconnect Network Path activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: d697232c-7604-4e8e-bde9-1d8e55a1c220
caps.latest.revision: 11
author: Jeronika-MS
ms.author: v-gajeronika
---
# Disconnect Network Path

The Disconnect Network Path activity allows you to disconnect a network path. You can disconnect network paths you mapped using the [Map Network Path](map-network-path.md) activity or using another method.  

## Configure the Disconnect Network Path Activity

 Before you configure the Disconnect Network Path activity, you need to determine the network path you want to disconnect.  

> [!NOTE]
> You can't set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

 Use the following information to configure the Disconnect Network Path activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Network path**|Enter the name of the network path that you want to disconnect, or select the ellipsis button **(...)** and browse for it.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Network path|The network path you're disconnecting.|
