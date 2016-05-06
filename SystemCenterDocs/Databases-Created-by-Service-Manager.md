---
title: Databases Created by Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7aa3ae77-88e7-4ff8-bb63-814286b7089f
---
# Databases Created by Service Manager
Before starting the installation of [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)], you may want to meet with your SQL Server administration team and discuss the impact that [!INCLUDE[smshort12](./Token/smshort12_md.md)] will have on your computers running SQL Server—specifically, the databases that will be created. The databases that are created by a deployment of [!INCLUDE[smshort12](./Token/smshort12_md.md)] are listed in the following table.

|[!INCLUDE[smshort12](./Token/smshort12_md.md)] parts|Database name|Contents|
|---------------------------------------------------------|-----------------|------------|
|[!INCLUDE[smshort12](./Token/smshort12_md.md)] database|[!INCLUDE[smshort12](./Token/smshort12_md.md)]|Configuration Items, Work Items, Incidents|
|[!INCLUDE[smshort12](./Token/smshort12_md.md)] data warehouse|DWStagingAndConfig<br /><br />DWRepository<br /><br />DWDataMart<br /><br />DWASDataBase<br /><br />OMDWDataMart<br /><br />CMDWDataMart|These first three databases make up the data warehouse. The extract process populates the DWStagingAndConfig database, which is transformed into a proper format in the DWRepository database, which, through the load process, becomes the content for the DWDataMart database.<br /><br />The DWASDatabase is used by SQL Server Analysis Services \(SSAS\) and stores Microsoft Online Analytical Processing \(OLAP\) cubes.<br /><br />The OMDWDataMart and CMDWDataMart databases are for collecting data from Operations Manager and Configuration Manager, respectively.|

> [!IMPORTANT]
> For this release, [!INCLUDE[smshort12](./Token/smshort12_md.md)] does not support case\-sensitive instance names. Setup will display a warning if you attempt to install [!INCLUDE[smshort12](./Token/smshort12_md.md)] on a case\-sensitive instance of Microsoft SQL Server.


