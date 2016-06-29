---
title: System Center 2012 - Service Manager Parts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f286c692-7648-4f78-a510-fb7e5553b04d
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
# System Center 2012 - Service Manager Parts
There are six major parts of a [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] installation, as described in the following table.  
  
###  
  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] part|Description|  
|--------------------------------|-----------------|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server|Contains the main software part of a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation. You can use the  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server to manage incidents, changes, users, and tasks.|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|The database that contains  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] configuration items \(CI\) from the IT Enterprise; work items, such as incidents, change requests, and the configuration for the product itself. This is the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] implementation of a Configuration Management Database \(CMDB\).|  
|Data warehouse management server|The computer that hosts the server piece of the data warehouse.|  
|Data warehouse databases|Databases that provide long\-term storage of the business data that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] generates. These databases are also used for reporting.|  
|[!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]|The user interface \(UI\) piece that is used by both the help desk analyst and the help desk administrator to perform [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] functions, such as incidents, changes, and tasks. This part is installed automatically when you deploy a  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server. In addition, you can manually install the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] as a stand\-alone part on a computer.|  
|[!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]|A web\-based interface into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].|  
  
> [!IMPORTANT]  
>  All computers that host any part of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] must be domain joined.