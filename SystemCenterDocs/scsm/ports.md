---
title: Port assignments for System Center - Service Manager
description: Learn about the port assignments used by System Center - Service Manager.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 04/21/2025
ms.subservice: service-manager
ms.topic: concept-article
ms.custom: engagement-fy24
---

# Port assignments for System Center - Service Manager


In this article, you'll learn about the port assignments used by System Center - Service Manager.

As part of your security infrastructure, you may want to keep track of port numbers that are used throughout your System Center - Service Manager environment. And while these port numbers aren't configurable, you can review the following table that lists port numbers that are used between the parts of Service Manager. You will want to ensure that these firewall ports are opened on computers that host Service Manager.  

## Port assignments  

|Component (piece A)|Port number/direction|Component (piece B)|  
|-----------------------------------|-------------------------------|-----------------------------------|  
|Service Manager console|5724 \-\-\-\>|Service Manager management server\*|  
|Service Manager console|5724 \-\-\-\>|Data warehouse management server|  
|Service Manager management server|1433 \-\-\-\>|Remote Service Manager database|  
|Service Manager management server|5724 \-\-\-\>|Data warehouse server|  
|Service Manager management server|5724 \-\-\-\>|Operations Manager Alert and CI connectors|  
|Service Manager management server|389 \-\-\-\>|Active Directory Connector|  
|Service Manager management server|1433 \-\-\-\>|Configuration Manager Connector|  
|Data warehouse management server|1433 \-\-\-\>|Remote data warehouse database server|  
|Data warehouse management server|1433 \-\-\-\>|Remote Service Manager database server|  
|Data warehouse management server|2383 \-\-\-\>|SQL Server Analysis Services\*\*|  
|SQL reporting service server|1433 \-\-\-\>|Remote data warehouse database server|  
|Web browser|80 \-\-\-\>|SQL Server Reporting Services \(SSRS\)|  

 \* Includes initial Service Manager management server and subsequent Service Manager management servers  

 \*\* Port 2383 is the default port for SQL Server Analysis Services \(SSAS\). However, the port number can be changed. For more information, see [Configure Windows Firewall for Analysis Services Access](/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access?viewFallbackFrom=sql-server-ver15).  

## Next steps

[Prepare for Service Manager deployment](prepare-deploy.md).
