---
title: System Center - Service Manager parts
description: Learn about the six major parts of System Center - Service Manager.
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: concept-article
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency2, engagement-fy24
---

# System Center - Service Manager parts



There are six major parts of a System Center - Service Manager installation, as described in the following table.  

|Service Manager part|Description|  
|--------------------------------|-----------------|  
|Service Manager management server|Contains the main software part of a Service Manager installation. You can use the Service Manager management server to manage incidents, changes, users, and tasks.|  
|Service Manager database|The database that contains Service Manager configuration items \(CI\) from the IT Enterprise; work items, such as incidents, change requests, and the configuration for the product itself. This is the Service Manager implementation of a Configuration Management Database \(CMDB\).|  
|Data warehouse management server|The computer that hosts the server piece of the data warehouse.|  
|Data warehouse databases|Databases that provide long\-term storage of the business data that Service Manager generates. These databases are also used for reporting.|  
|Service Manager console|The user interface \(UI\) piece that is used by both the help desk analyst and the help desk administrator to perform Service Manager functions, such as incidents, changes, and tasks. This part is installed automatically when you deploy a  Service Manager management server. In addition, you can manually install the Service Manager console as a standalone part on a computer.|  
|Self-Service Portal|A web\-based interface into Service Manager.|  

>[!IMPORTANT]
>All computers that host any part of Service Manager must be domain-joined.
