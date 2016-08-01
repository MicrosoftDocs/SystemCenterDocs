---
title: Databases Created by System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ca01c52-86ea-4ba2-afce-00c8453a4df5
---

# Databases Created by System Center 2016 - Service Manager

Before starting the installation of System Center 2016 - Service Manager, you may want to meet with your SQL Server administration team and discuss the impact that Service Manager will have on your computers running SQL Server-specifically, the databases that will be created. The databases that are created by a deployment of Service Manager are listed in the following table.  

|Service Manager parts|Database name|Contents|  
|---------------------------------|-------------------|--------------|  
|Service Manager database|Service Manager|Configuration Items, Work Items, Incidents|  
|Service Manager data warehouse|DWStagingAndConfig<br /><br /> DWRepository<br /><br /> DWDataMart<br /><br /> DWASDataBase<br /><br /> OMDWDataMart<br /><br /> CMDWDataMart|These first three databases make up the data warehouse. The extract process populates the DWStagingAndConfig database, which is transformed into a proper format in the DWRepository database, which, through the load process, becomes the content for the DWDataMart database.<br /><br /> The DWASDatabase is used by SQL Server Analysis Services \(SSAS\) and stores Microsoft Online Analytical Processing \(OLAP\) cubes.<br /><br /> The OMDWDataMart and CMDWDataMart databases are for collecting data from Operations Manager and Configuration Manager, respectively.|  

> [!IMPORTANT]  
>  For this release, Service Manager does not support case\-sensitive instance names. Setup will display a warning if you attempt to install Service Manager on a case\-sensitive instance of Microsoft SQL Server.
