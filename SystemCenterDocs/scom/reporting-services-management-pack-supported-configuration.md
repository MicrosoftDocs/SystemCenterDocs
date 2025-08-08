---
ms.topic: article 
ms.assetid: 3e7cc6b6-1d9e-4299-90c9-5427d6a9e56b
title: Scope and Supported Configuration in Management Pack for SQL Server Reporting Services
description: This article explains the scope and supported configuration for Management Pack for SQL Server Reporting Services
author: epomortseva
ms.author: v-vlchernov
manager: evansma
ms.date: 03/31/2025
ms.service: system-center
ms.subservice: operations-manager
---

# Scope and Supported Configuration in Management Pack for SQL Server Reporting Services



Management Pack for SQL Server Reporting Services is version-agnostic and supports discovery and monitoring of SQL Server Reporting Services 2012 through 2022 and higher and Power BI Report Server.

This article explains the scope and supported configuration for Management Pack for SQL Server Reporting Services.

## SQL Server Reporting Services Features

The following is a list of features and configurations supported in Management Pack for SQL Server Reporting Services:

- SQL Server Reporting Services Instance (Native Mode)

- SQL Server Reporting Services Scale-out deployment

- Power BI Report Server - Verified with build 15.0.1110.120

  The management pack treats Power BI Report Server as a special kind of SQL Server Reporting Services and provides the same monitoring for Power BI Report Server instances as it does for Reporting Services instances. In this guide, we'll use SSRS or Reporting Services, but each term is intended for both SQL Server Reporting Services and Power BI Report Server.

## System Center Operations Manager

::: moniker range="<=sc-om-2022"

Management Pack for SQL Server Analysis Services supports the following versions of System Center Operations Manager:

- System Center Operations Manager 2012 R2
  
  Due to the [Lifecycle Policy](/lifecycle/products/microsoft-system-center-2012-r2-operations-manager), this version is no longer being tested.
  
- System Center Operations Manager 2016
- System Center Operations Manager 2019
- System Center Operations Manager 2022
- System Center Operations Manager 2025

::: moniker-end

::: moniker range="sc-om-2025"

- System Center Operations Manager 2019
- System Center Operations Manager 2022
- System Center Operations Manager 2025

::: moniker-end

A dedicated Operations Manager management group isn't required for this management pack.

## Supported Operating Systems and Platforms

Management Pack for SQL Server Reporting Services supports the following 64-bit operating systems and platforms:

::: moniker range="<=sc-om-2022"

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019
- Windows Server 2022

::: moniker-end

::: moniker range="sc-om-2025"
- Windows Server 2019
- Windows Server 2022
- Windows Server 2025

::: moniker-end

Localized versions of Windows Server are also supported.
