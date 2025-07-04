---
title: Get Dial-up Status
description: This article describes the functionality of Get Dial-up Status activity.
ms.custom: UpdateFrequency2, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: ab465f97-ef96-41b8-bae5-57c5413af14a
caps.latest.revision: 5
author: jyothisuri
ms.author: jsuri
---
# Get Dial-up Status

The Get Dial-up Status activity retrieves the status of a dial-up or VPN network connection on the Runbook server. For more information on creating a network connection in Windows Server 2008, see [Establish Network Connections](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/gg252606(v=ws.10))  

## Configure the Get Dial-up Status Activity

 Use the following information to configure the Get Dial-up Status activity.  

> [!NOTE]
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

### Connection Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Dial-up or VPN entry**|Enter the name of the entry as entered in the address book, or select the ellipsis **(…)** button and select the entry from the Remote Access Phone Book.|  

### Published Data

The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Dial-up or VPN name|The name assigned to the dial-up connection|  
|Line status|Indicates whether the network connection is connected or disconnected|
