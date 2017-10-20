---
title: Service Manager parts
description: Learn about the six major parts of Service Manager.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f286c692-7648-4f78-a510-fb7e5553b04d
---

# System Center 2016 - Service Manager parts

>Applies To: System Center 2016 - Service Manager

There are six major parts of a System Center 2016 - Service Manager installation, as described in the following table.  


|Service Manager part|Description|  
|--------------------------------|-----------------|  
|Service Manager management server|Contains the main software part of a Service Manager installation. You can use the  Service Manager management server to manage incidents, changes, users, and tasks.|  
|Service Manager database|The database that contains  Service Manager configuration items \(CI\) from the IT Enterprise; work items, such as incidents, change requests, and the configuration for the product itself. This is the Service Manager implementation of a Configuration Management Database \(CMDB\).|  
|Data warehouse management server|The computer that hosts the server piece of the data warehouse.|  
|Data warehouse databases|Databases that provide long\-term storage of the business data that Service Manager generates. These databases are also used for reporting.|  
|Service Manager console|The user interface \(UI\) piece that is used by both the help desk analyst and the help desk administrator to perform Service Manager functions, such as incidents, changes, and tasks. This part is installed automatically when you deploy a  Service Manager management server. In addition, you can manually install the Service Manager console as a stand\-alone part on a computer.|  
|Self-Service Portal|A web\-based interface into Service Manager.|  

>[!IMPORTANT]
All computers that host any part of Service Manager must be domain-joined.
