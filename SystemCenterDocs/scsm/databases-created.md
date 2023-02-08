---
title: Databases creation by System Center
description: This article describes the databases that are created by Service Manager during installation.
manager: mkluck
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: article
---

# Databases created by System Center - Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

Before you start the installation of System Center - Service Manager, you may want to meet with your SQL Server administration team to discuss the effect Service Manager will have on your computers running SQL Server, specifically the databases that will be created. The databases that are created by the deployment of Service Manager are listed in the following table.  

|Service Manager parts|Database name|Contents|  
|---------------------------------|-------------------|--------------|  
|Service Manager database|Service Manager|Configuration Items, Work Items, Incidents|  
|Service Manager data warehouse|DWStagingAndConfig<br /><br /> DWRepository<br /><br /> DWDataMart<br /><br /> DWASDataBase<br /><br /> OMDWDataMart<br /><br /> CMDWDataMart|These first three databases make up the data warehouse. The extract process populates the DWStagingAndConfig database, which is transformed into a proper format in the DWRepository database, which, through the load process, becomes the content for the DWDataMart database.<br /><br /> The DWASDatabase is used by SQL Server Analysis Services \(SSAS\) and stores Microsoft Online Analytical Processing \(OLAP\) cubes.<br /><br /> The OMDWDataMart and CMDWDataMart databases are for collecting data from Operations Manager and Configuration Manager, respectively.|  

> [!IMPORTANT]  
>  Service Manager doesn't support case\-sensitive instance names. Setup will display a warning if you attempt to install Service Manager on a case\-sensitive instance of Microsoft SQL Server.

## Next steps

- To learn about the port numbers that are used in your Service Manager environment, review [port assignments for Service Manager](~/scsm/ports.md).
