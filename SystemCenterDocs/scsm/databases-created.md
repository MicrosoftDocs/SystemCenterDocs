---
title: Databases creation by System Center
description: This article describes the databases that are created by Service Manager during installation.
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1825-days
ms.subservice: service-manager
ms.topic: concept-article
ms.custom: UpdateFrequency5, engagement-fy24
---

# Databases created by System Center - Service Manager



Before you start the installation of System Center - Service Manager, you may want to meet with your SQL Server administration team to discuss the effect Service Manager has on your computers running SQL Server, specifically the databases that are created. The databases that are created by the deployment of Service Manager are listed in the following table.  

|Service Manager parts|Database name|Contents|  
|---------------------------------|-------------------|--------------|  
|Service Manager database|Service Manager|Configuration Items, Work Items, Incidents|  
|Service Manager data warehouse|DWStagingAndConfig<br /><br /> DWRepository<br /><br /> DWDataMart<br /><br /> DWASDataBase<br /><br /> OMDWDataMart<br /><br /> CMDWDataMart|These first three databases make up the data warehouse. The extract process populates the DWStagingAndConfig database, which is transformed into a proper format in the DWRepository database, which, through the load process, becomes the content for the DWDataMart database.<br /><br /> The DWASDatabase is used by SQL Server Analysis Services \(SSAS\) and stores Microsoft Online Analytical Processing \(OLAP\) cubes.<br /><br /> The OMDWDataMart and CMDWDataMart databases are for collecting data from Operations Manager and Configuration Manager, respectively.|  

> [!IMPORTANT]  
> Service Manager doesn't support case\-sensitive instance names. Setup will display a warning if you attempt to install Service Manager on a case\-sensitive instance of Microsoft SQL Server.

## Next steps

- To learn about the port numbers that are used in your Service Manager environment, review [port assignments for Service Manager](~/scsm/ports.md).
