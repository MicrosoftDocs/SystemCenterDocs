---
ms.assetid: 3e7cc6b6-1d9e-4299-90c9-5427d6a9e56b
title: Scope and supported configuration in Management Pack for SQL Server Reporting Services
description: This article explains the scope and supported configuration for Management Pack for SQL Server Reporting Services
author: vchvlad
ms.author: v-vchernov
manager: evansma
ms.date: 11/25/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for SQL Server Reporting Services

Management Pack for SQL Server Reporting Services is version-agnostic and supports discovery and monitoring of SQL Server Reporting Services 2012 through 2022 and higher as well as Power BI Report Server.

## SQL Server Reporting Services Features

The following is a list of features and configurations supported in Management Pack for SQL Server Reporting Services:

- SQL Server Reporting Services Instance (Native Mode)

- SQL Server Reporting Services Scale-out deployment

- Power BI Report Server - Verified with build 15.0.1110.120

  The management pack treats Power BI Report Server as a special kind of SQL Server Reporting Services and provides the same monitoring for Power BI Report Server instances as it does for Reporting Services instances. In this guide, we will use SSRS or Reporting Services, but each term is intended for both SQL Server Reporting Services and Power BI Report Server.

## System Center Operations Manager

Management Pack for SQL Server Analysis Services supports the following versions of System Center Operations Manager:

- System Center Operations Manager 2012 R2
  
  Due to the [Lifecycle Policy](/lifecycle/products/microsoft-system-center-2012-r2-operations-manager), this version is no longer being tested.
  
- System Center Operations Manager 2016
- System Center Operations Manager 1801
- System Center Operations Manager 1807
- System Center Operations Manager 2019
- System Center Operations Manager 2022

A dedicated Operations Manager management group is not required for this management pack.

## Supported Operating Systems and Platforms

Management Pack for SQL Server Reporting Services supports the following 64-bit operating systems and platforms:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019
- Windows Server 2022

Localized versions of Windows Server are also supported.
