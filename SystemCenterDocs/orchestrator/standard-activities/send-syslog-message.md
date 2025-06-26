---
title: Send Syslog Message 
description: This article provides information about the Send Syslog Message activity
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: e4531b9d-4434-4ad9-8f16-5497eb3e86e4
caps.latest.revision: 12
author: jyothisuri
ms.author: jsuri
---
# Send Syslog Message

The Send Syslog Message activity creates a message on the Syslog server that you specify. You can use this activity to create audit logs on the Syslog server that document any problems that occur while trying to correct issues using an automated runbook.  

## Configuring the Send Syslog Message Activity

 Use the following information to configure the Send Syslog Message activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer that contains the Syslog server that you're writing the message to. You can also use the ellipsis **(...)** button to browse for the computer.|  
|**Text**|Enter the message of the event log entry.|  
|**Priority**|Select the priority from the dropdown menu that is appropriate for this message.|  
|**Facility**|Select the facility from the dropdown menu that is appropriate for this message.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer|The computer where the Syslog server is located.|  
|Priority|The priority of the message.|  
|Facility|The facility that the message belongs to.|  
|Message|The text of the message.|
