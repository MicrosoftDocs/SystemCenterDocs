---
title: Hardware Requirements for System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f63bb78a-9f4e-4cc5-bdcb-a180c8eeda81
---

# Hardware Requirements for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This topic describes the hardware requirements for System Center 2016 - Service Manager.  

## Hardware Requirements  

The following table lists the recommended hardware requirements for the individual parts of Service Manager. These computers can be physical servers or virtual servers.  


### Hardware requirements table  

| Service Manager Role | requirement |
|---|---|  
|Service Manager database|8\-core 2.66 gigahertz \(GHz\) CPU<br /><br /> 8 gigabytes \(GB\) of RAM for 20,000 users, 32 GB of RAM for 50,000 users \(See the [Hardware Performance](plan-hardware-performance.md) section in this guide.\)<br /><br /> 80 GB of available disk space<br /><br /> RAID Level 1 or Level 10 drive\*|  
|Service Manager management server|4\-Core 2.66 GHz CPU<br /><br /> 8 GB of RAM \(See the [Hardware Performance](plan-hardware-performance.md) section in this guide.\)<br /><br /> 10 GB of available disk space|  
|Service Manager console|2\-core 2.0 GHz CPU<br /><br /> 4 GB of RAM<br /><br /> 10 GB of available disk space|  
|Data warehouse management server|4\-Core 2.66 GHz CPU<br /><br /> 8 GB of RAM \(See the [Hardware Performance](plan-hardware-performance.md) section in this guide.\)<br /><br /> When a data warehouse management group and SQL Server Analysis Services are hosted on a single server, it should contain at least 16 GB RAM.<br /><br /> 10 GB of available disk space|  
|Data warehouse databases|8\-core 2.66 GHz CPU<br /><br /> 8 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users \(See the [Hardware Performance](plan-hardware-performance.md) section in this guide.\)<br /><br /> 400 GB of available disk space<br /><br /> RAID Level 1 or Level \(1\+0\) drive|  
|Self-Service Portal: Web Content Server with SharePoint Web Parts|8\-Core 2.66 GHz CPU<br /><br /> 8\-core, 64\-bit CPU for medium deployments<br /><br /> 16 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users \(See the [Hardware Performance](plan-hardware-performance.md) section in this guide.\)<br /><br /> 80 GB of available hard disk space|  

\* For more information, see [RAID levels and Microsoft SQL Server](http://go.microsoft.com/fwlink/p/?LinkID=134073).  
