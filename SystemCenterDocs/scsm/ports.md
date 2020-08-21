---
title: Port assignments for System Center - Service Manager
description: Learn about the port assignments used by System Center - Service Manager.
manager: carmonm
ms.prod: system-center
author: JYOTHIRMAISURI
ms.author: v-jysur
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: article
---

# Port assignments for System Center - Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

As part of your security infrastructure, you may want to keep track of port numbers that are used throughout your System Center - Service Manager environment. And while these port numbers are not configurable, you can review the following table that lists port numbers that are used between the parts of Service Manager. You will want to ensure that these firewall ports are opened on computers that host Service Manager.  

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

 \*\* Port 2383 is the default port for SQL Server Analysis Services \(SSAS\). However, the port number can be changed. For more information, see [Configure Windows Firewall for Analysis Services Access](https://go.microsoft.com/fwlink/p/?LinkID=216892).  

## Next steps

- [Prepare for Service Manager deployment](prepare-deploy.md).
