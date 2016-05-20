---
title: Port Assignments for Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5dc3497-2d5a-4d70-9410-d4365b85b48f
---
# Port Assignments for Service Manager
As part of your security infrastructure, you may want to keep track of port numbers that are used throughout your [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] environment. And while, in this release, these port numbers are not configurable, you can review the following table that lists port numbers that are used between the parts of [!INCLUDE[smshort12](Token/smshort12_md.md)]. You will want to ensure that these firewall ports are opened on computers that host [!INCLUDE[smshort12](Token/smshort12_md.md)].

### Port Assignments

|[!INCLUDE[smshort12](Token/smshort12_md.md)] piece A|Port number and direction|[!INCLUDE[smshort12](Token/smshort12_md.md)] piece B|
|-----------------------------------------------------------|-----------------------------|-----------------------------------------------------------|
|[!INCLUDE[smcons](Token/smcons_md.md)]|5724 \-\-\->|[!INCLUDE[smshort12](Token/smshort12_md.md)] management server\*|
|[!INCLUDE[smcons](Token/smcons_md.md)]|5724 \-\-\->|Data warehouse management server|
|[!INCLUDE[smshort12](Token/smshort12_md.md)] management server|1433 \-\-\->|Remote [!INCLUDE[smshort12](Token/smshort12_md.md)] database|
|[!INCLUDE[smshort12](Token/smshort12_md.md)] management server|5724 \-\-\->|Data warehouse server|
|[!INCLUDE[smshort12](Token/smshort12_md.md)] management server|5724 \-\-\->|Operations Manager 2007 Alert and CI connectors|
|[!INCLUDE[smshort12](Token/smshort12_md.md)] management server|389 \-\-\->|Active Directory Connector|
|[!INCLUDE[smshort12](Token/smshort12_md.md)] management server|1433 \-\-\->|Configuration Manager Connector|
|Data warehouse management server|1433 \-\-\->|Remote data warehouse database server|
|Data warehouse management server|1433 \-\-\->|Remote [!INCLUDE[smshort12](Token/smshort12_md.md)] database server|
|Data warehouse management server|2383 \-\-\->|SQL Server Analysis Services\*\*|
|SQL reporting service server|1433 \-\-\->|Remote data warehouse database server|
|Web browser|80 \-\-\->|SQL Server Reporting Services \(SSRS\)|
|Web browser|\[setup\*\*\*\] \-\-\->|SharePoint Web Parts server|
|Web browser|\[setup\*\*\*\] \-\-\->|Web content server|
|Web content server|1433 \-\-\->|[!INCLUDE[smshort12](Token/smshort12_md.md)] database|

\* Includes initial [!INCLUDE[smshort12](Token/smshort12_md.md)] management server and subsequent [!INCLUDE[smshort12](Token/smshort12_md.md)] management servers

\*\* Port 2383 is the default port for SQL Server Analysis Services \(SSAS\). However, the port number can be changed. For more information, see [Configure Windows Firewall for Analysis Services Access](http://go.microsoft.com/fwlink/p/?LinkID=216892).

\*\*\* The port number that is used between the browser and the SharePoint Web Parts server and the web content server is configured during installation of the [!INCLUDE[smssp](Token/smssp_md.md)].


