---
title: "Monitor Computer-IP | Microsoft Docs"
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
ms.assetid: eee8ce17-c286-41ac-9736-00e96fa78f71
caps.latest.revision: 16
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Monitor Computer/IP

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The Monitor Computer/IP activity will send a ping to a remote computer or IP address and wait for a response. You can configure the Monitor Computer/IP activity to invoke your runbook if the computer is either reachable or unreachable. The Monitor Computer/IP activity can be used to invoke runbooks that will automatically notify administrators when a vital system has become unreachable on the network.  

## Configuring the Monitor Computer/IP Activity  
 Before you configure the Monitor Computer/IP activity, you will need to determine the following:  

-   The computer you are monitoring.  

-   Whether you are waiting for the computer to become reachable or waiting for it become not reachable.  

> [!IMPORTANT]
>  You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

 Use the following information to configure the Monitor Computer/IP activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Type the name of the computer that you are monitoring. You can also browse for the computer using the ellipsis **(...)** button.|  
|**The computer is not reachable**|Select to invoke the Monitor Computer/IP activity when the computer that you are monitoring cannot be reached using a ping.|  
|**The computer is reachable**|Select to run the Monitor Computer/IP activity when the computer that you are monitoring can be reached using a ping.|  
|**Test frequency**|Specify the amount of time between each ping to the **Computer**.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer to ping|The computer that is being monitored.|  
|Percentage of packets received|The percentage of packets that were received back from the ping.|
