---
title: Databases Created by System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ca01c52-86ea-4ba2-afce-00c8453a4df5
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
# Databases Created by System Center 2012 - Service Manager
Before starting the installation of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you may want to meet with your SQL Server administration team and discuss the impact that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] will have on your computers running SQL Server—specifically, the databases that will be created. The databases that are created by a deployment of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] are listed in the following table.  
  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] parts|Database name|Contents|  
|---------------------------------|-------------------|--------------|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|Configuration Items, Work Items, Incidents|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse|DWStagingAndConfig<br /><br /> DWRepository<br /><br /> DWDataMart<br /><br /> DWASDataBase<br /><br /> OMDWDataMart<br /><br /> CMDWDataMart|These first three databases make up the data warehouse. The extract process populates the DWStagingAndConfig database, which is transformed into a proper format in the DWRepository database, which, through the load process, becomes the content for the DWDataMart database.<br /><br /> The DWASDatabase is used by SQL Server Analysis Services \(SSAS\) and stores Microsoft Online Analytical Processing \(OLAP\) cubes.<br /><br /> The OMDWDataMart and CMDWDataMart databases are for collecting data from Operations Manager and Configuration Manager, respectively.|  
  
> [!IMPORTANT]  
>  For this release, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] does not support case\-sensitive instance names. Setup will display a warning if you attempt to install [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] on a case\-sensitive instance of Microsoft SQL Server.