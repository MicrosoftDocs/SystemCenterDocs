---
title: Disconnect Network Path
description: This article describes the Disconnect Network Path activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/27/2023
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d697232c-7604-4e8e-bde9-1d8e55a1c220
caps.latest.revision: 11
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---
# Disconnect Network Path

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The Disconnect Network Path activity allows you to disconnect a network path. You can disconnect network paths you mapped using the [Map Network Path](map-network-path.md) activity or using another method.  

## Configuring the Disconnect Network Path Activity  
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