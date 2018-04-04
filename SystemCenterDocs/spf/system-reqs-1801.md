---
ms.assetid: d4d662cd-de11-4f4b-bff1-cbe0ea927f6f
title: SPF system requirements for 1801
description: This article provides information about hardware and software system requirements for SPF 1801
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  02/05/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  service-provider-foundation
monikerRange: 'sc-spf-1801'
---

# System requirements for System Center 1801 - Service Provider Foundation

This article describes the hardware and software requirements for System Center 1801 - Service Provider Foundation (SPF).


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

**SQL version** | **Supported**
--- | ---
**SQL Server 2008**| N
**SQL Server 2012 and SPs as detailed [here](https://support.microsoft.com/en-in/lifecycle/search?alpha=SQL%20server%202012%20service%20pack)** | Y
**SQL Server 2014 and SPs as detailed [here](https://support.microsoft.com/en-in/lifecycle/search?alpha=SQL%20server%202014%20service%20pack)** | Y
**SQL Server 2016 and SPs as detailed [here](https://support.microsoft.com/en-in/lifecycle/search?alpha=SQL%20server%202016%20service%20pack)** | Y

## Installation components

These components should be installed on the server, before you install VMM.

**installation** | **Supported**
--- | ---
**PowerShell** | PowerShell 4.0, 5.0
**.NET** | 4.5.2, 4.6





## Next steps

[Learn more about SPF?](~/spf/overview.md)
