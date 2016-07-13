---
title: Hardware Requirements for System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f63bb78a-9f4e-4cc5-bdcb-a180c8eeda81
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Hardware Requirements for System Center 2012 - Service Manager
This topic describes the hardware requirements for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
## Hardware Requirements  
 The following table lists the recommended hardware requirements for the individual parts of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. These computers can be physical servers or virtual servers.  
  
 [!INCLUDE[sc2012sp1note](../../../sm/plan/planning/includes/sc2012sp1note_md.md)] The hardware requirements for [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] in [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)] are unchanged from its initial release.  
  
### Hardware requirements table  
  
|||  
|-|-|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|8\-core 2.66 gigahertz \(GHz\) CPU<br /><br /> 8 gigabytes \(GB\) of RAM for 20,000 users, 32 GB of RAM for 50,000 users \(See the [Hardware Performance](../../../sm/plan/planning/Hardware-Performance.md) section in this guide.\)<br /><br /> 80 GB of available disk space<br /><br /> RAID Level 1 or Level 10 drive\*|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server|4\-Core 2.66 GHz CPU<br /><br /> 8 GB of RAM \(See the [Hardware Performance](../../../sm/plan/planning/Hardware-Performance.md) section in this guide.\)<br /><br /> 10 GB of available disk space|  
|[!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]|2\-core 2.0 GHz CPU<br /><br /> 4 GB of RAM<br /><br /> 10 GB of available disk space|  
|Data warehouse management server|4\-Core 2.66 GHz CPU<br /><br /> 8 GB of RAM \(See the [Hardware Performance](../../../sm/plan/planning/Hardware-Performance.md) section in this guide.\)<br /><br /> When a data warehouse management group and SQL Server Analysis Services are hosted on a single server, it should contain at least 16 GB RAM.<br /><br /> 10 GB of available disk space|  
|Data warehouse databases|8\-core 2.66 GHz CPU<br /><br /> 8 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users \(See the [Hardware Performance](../../../sm/plan/planning/Hardware-Performance.md) section in this guide.\)<br /><br /> 400 GB of available disk space<br /><br /> RAID Level 1 or Level \(1\+0\) drive|  
|[!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]: Web Content Server with SharePoint Web Parts|8\-Core 2.66 GHz CPU<br /><br /> 8\-core, 64\-bit CPU for medium deployments<br /><br /> 16 GB of RAM for 20,000 users, 32 GB of RAM for 50,000 users \(See the [Hardware Performance](../../../sm/plan/planning/Hardware-Performance.md) section in this guide.\)<br /><br /> 80 GB of available hard disk space|  
  
 \* For more information, see [RAID levels and Microsoft SQL Server](http://go.microsoft.com/fwlink/p/?LinkID=134073).  
  
 \*\* Hardware requirements are based on SharePoint specifications. For more information, see [Hardware and Software Requirements \(SharePoint Server 2010\)](http://go.microsoft.com/fwlink/p/?LinkID=219606).