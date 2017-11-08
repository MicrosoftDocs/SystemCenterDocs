---
title: System Requirements for Service Manager
manager: carmonm
description: The article describes Service Manager system requirements.
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 02/02/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8b7da0ea-ebfb-4217-b650-929a0f7fb14b
---

# System requirements for System Center 2016 - Service Manager

The article describes general performance and scalability guidance for System Center 2016 - Service Manager and recommends hardware configurations for a variety of workloads. Because System Center 2016 is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.  

## Capacity limits for Service Manager

Read [Configurations for deployment scenarios](deploy-topo-scenarios.md) to learn about the tested capacity limits of Service Manager.

## Hardware

|System Center 2016 servers|Processor (min)|Processor (rec)|RAM (min)|RAM (rec)|Hard drive space (min)|Hard drive space (rec)|
|---------------------------------|---------------------|---------------------|---------------|---------------|----------------------------|----------------------------|
|**Service Manager** Management Server|4-Core 2.66 GHz CPU|4-Core 2.66 GHz CPU|8 GB|8 GB|10 GB|10 GB|
|**Service Manager** Database|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|32 GB|80 GB|80 GB|
|**Service Manager** Data Warehouse Management Server|4-Core 2.66 GHz CPU|4-Core 2.66 GHz CPU|8 GB|16 GB|10 GB|10 GB|
|**Service Manager** Data Warehouse Databases|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|32 GB|400 GB|400 GB|
|**Service Manager** Console|2-Core 2 GHz CPU|2-Core 2 GHz CPU|4 GB|4 GB|10 GB|10 GB|
|**Service Manager** Self-Service Portal (standalone)|4-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|16 GB|80 GB|80 GB|
|**Service Manager** Self-Service Portal + Secondary Management Server (Recommended)|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|16 GB|32 GB|80 GB|80 GB|

## Server operating system

The following versions of Windows Server operating system are supported.

|System Center  component|Windows Server 2012 Standard, Datacenter|Windows Server 2012 R2 Standard, Datacenter|Windows Server 2016|Windows Server 2016 (Server with Desktop Experience)|Windows Server 2016 Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|
|**Service Manager** Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Data Warehouse Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Database or Data Warehouse Database||&#8226;|&#8226;|&#8226;||
|**Service Manager** Self-Service Portal (HTML 5)||&#8226;|&#8226;|&#8226;|&nbsp;|

Service Manager has a number of software requirements, depending on the type of component to install. See [Software requirements for Service Manager](sm-software-reqs.md) for more information.


## Client operating system

The following versions of Windows client operating system are supported for the Service Manager console.

|System Center client-side components|Windows&reg; 7|Windows&reg; 8|Windows&reg; 8.1|Windows Server&reg; 2008 R2 SP1|Windows Server&reg; 2012|Windows Server&reg; 2012 R2 Standard, Datacenter|Windows 10 Enterprise|Windows Server&reg; 2016 Standard, Datacenter|
|-----------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|-----------------------------------------------------------------|-----------------------------------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
|**Service Manager** Console|&#8226;|&#8226;|&#8226;|||&#8226;|&#8226;|&#8226;|


## .Net Versions supported

The following versions of .Net are supported for Service Manager.

|System Center 2016 component|.NET 3.5 SP1|.NET 4|.NET 4.5|.NET 4.5.1|.NET 4.5.2|.NET 4.6|
|-----------------------------------|----------------|----------|------------|--------------|--------------|------------|
|**Service Manager** Management Server|&#8226;| | |&#8226;| | |
|**Service Manager** Data Warehouse Management Server|&#8226;| | |&#8226;| | |
|**Service Manager** console|&#8226;| | |&#8226;| | |
|**Service Manager** Self\-Service Portal|&#8226;| | |&#8226;| | &nbsp; |

## PowerShell Versions supported

The following versions of PowerShell are supported for Service Manager.

|System Center Component|Windows PowerShell 2.0|Windows PowerShell 3.0|Windows PowerShell 4.0|Windows PowerShell 5.0|
|---------------------------|--------------------------|--------------------------|-----------------------------------------------|-----------------------------------------------|
|**Service Manager** Console|||&#8226;|&#8226;|
|**Service Manager** Management Server|||&#8226;|&#8226;|
|**Service Manager** Data Warehouse Management Server|||&#8226;|&#8226;|


## Supported coexistence

To help simplify upgrades, you can use the following Service Manager 2016 connectors with System Center 2012 R2 components.

- System Center 2012 R2 Virtual Machine manager
- System Center 2012 R2 Orchestrator
- System Center 2012 R2 Operations Manager
- System Center 2012 R2 Configuration Manager (including SCCM 1511, 1602 and 1606)

## Next steps
- Read [Configurations for deployment scenarios](deploy-topo-scenarios.md) to learn about the tested limits of Service Manager.
- Read about Service Manager [hardware performance](plan-hardware-perf.md).
- Read about [SQL Server requirements](sm-sql-reqs.md).
