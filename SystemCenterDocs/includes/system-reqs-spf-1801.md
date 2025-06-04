---
ms.assetid: d4d662cd-de11-4f4b-bff1-cbe0ea927f6f
title: include file
description: include file to provide information about hardware and software system requirements for System Center  2016 - Service Provider Foundation
author: jyothisuri
ms.author: jsuri
ms.date:  06/14/2018
ms.topic:  include
ms.service:  system-center
ms.subservice:  service-provider-foundation
---

## System requirements for System Center 1801 - Service Provider Foundation

The following sections describe the hardware and software requirements for System Center 1801 - Service Provider Foundation (SPF).


## Hardware

**Hardware** | **Supported**
--- | ---
**Processor (minimum)** | 2.1 GHx dual core CPU or faster
**Processor (recommended)** | 2.1 GHx dual core CPU or faster
**RAM (minimum)** | 8 GB
**RAM (recommended)** | 16 GB


## Server operating system

**Operating system** | **Supported**
--- | --- | --- | ---
**Windows Server 2012 Standard/Datacenter** | N
**Windows Server 2012 R2 Standard/Datacenter** | N
**Windows Server 2016** | Y
**Windows Server 2016 (with desktop experience)** | Y
**Windows Server 2016 Nano** | N

## SQL Server

> [!NOTE]
> For the supported versions of SQL, use the service packs that are currently in support by Microsoft.

|                                                                 **SQL version**                                                                 | **Supported** |
|-------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
|                                                               **SQL Server 2008**                                                               |       N       |
| **SQL Server 2012 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2012)** |       Y       |
| **SQL Server 2014 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2014)** |       Y       |
| **SQL Server 2016 and SPs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)** |       Y       |

## Installation components

These components should be installed on the server, before you install VMM.

**Installation** | **Supported**
--- | ---
**PowerShell** | PowerShell 4.0, 5.0
**.NET** | 4.5.2, 4.6