---
title: "Send Event Log Message | Microsoft Docs"
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
ms.assetid: 02ca2b81-a6a5-444a-8ddd-f3695ca5afd4
caps.latest.revision: 10
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Send Event Log Message

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The Send Event Log Message activity creates an entry in the Windows Event Log within the Application folder. This activity can be used to create audit logs in the Windows Event Log that document any problems that occur while trying to correct issues by using an automated runbook.  

## Configuring the Send Event Log Message Activity  
 Before you configure the Send Event Log Message activity, you will need to determine the following:  

- The event message you are creating.  

- The severity of the event  

Use the following information to configure the Send Event Log Message activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Type the name of the computer that contains the Windows Event Log that you are writing to. You can also use the ellipsis **(...)** button to browse for the computer.|  
|**Message**|Type the message text of the event log entry.|  
|**Severity**|Select the severity level that is appropriate for this event.<br /><br /> You can select **Information**, **Warning**, or **Error**.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer|The computer where the event log message was created.|  
|Log entry description|The description of the event log message.|
