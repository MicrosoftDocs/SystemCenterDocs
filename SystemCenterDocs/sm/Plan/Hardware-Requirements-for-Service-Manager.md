---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Hardware Requirements for Service Manager
ms.technology:  service-manager
ms.assetid:  e13218d6-05f1-46d1-8f10-068a2497aacb
---

# Hardware Requirements for Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager


This topic describes the hardware requirements for System Center 2016 Technical Preview - Service Manager.


## Hardware Requirements


The following table lists the recommended hardware requirements for the individual parts of System Center 2016 Technical Preview - Service Manager. These computers can be physical servers or virtual servers.

The hardware requirements for Service Manager in are unchanged from its initial release.

## Hardware requirements table

|||
|---|---|
| System Center 2016 Technical Preview - Service Manager database | 8-core 2.66 gigahertz (GHz) CPU <br> 8 gigabytes (GB) of RAM for 20,000 users, 32 GB of RAM for 50,000 users <br> 80 GB of available disk space <br> RAID Level 1 or Level 10 drive&#42; |
| System Center 2016 Technical Preview - Service Manager management server | 4-Core 2.66 GHz CPU <br> 8 GB of RAM <br>  10 GB of available disk space |
| Service Manager console | 2-core 2.0 GHz CPU <br> 4 GB of RAM <br> 10 GB of available disk space |
| Data warehouse management server | 4-Core 2.66 GHz CPU <br> 8 GB of RAM <br> When a data warehouse management group and SQL Server Analysis Services are hosted on a single server, it should contain at least 16 GB RAM. <br> 10 GB of available disk space.|
| Data warehouse databases | 8-core 2.66 GHz CPU <br> 8 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users <br> 400 GB of available disk space <br> RAID Level 1 or Level (1+0) drive |
| Self-Service Portal: Web Content Server with SharePoint Web Parts | 8-Core 2.66 GHz CPU <br> 8-core, 64-bit CPU for medium deployments <br> 16 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users. <br> 80 GB of available hard disk space |



&#42; For more information, see [RAID levels and Microsoft SQL Server](http://go.microsoft.com/fwlink/p/?LinkID=134073).

&42;&42; Hardware requirements are based on SharePoint specifications. For more information, see [Hardware and Software Requirements (SharePoint Server 2010)](http://go.microsoft.com/fwlink/p/?LinkID=219606).
