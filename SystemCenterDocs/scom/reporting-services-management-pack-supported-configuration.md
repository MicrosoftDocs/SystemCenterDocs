---
ms.assetid: 3e7cc6b6-1d9e-4299-90c9-5427d6a9e56b
title: Scope and supported configuration in Management Pack for SQL Server Reporting Services
description: This article explains the scope and supported configuration for Management Pack for SQL Server Reporting Services
author: TDzakhov
ms.author: v-tdzakhov
manager: evansma
ms.date: 11/16/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for SQL Server Reporting Services

Management Pack for SQL Server Reporting Services is version-agnostic and supports discovery and monitoring of SQL Server Reporting Services 2012 through 2019 and higher as well as Power BI Report Server.

## Operating Systems and Platforms

Management Pack for SQL Server Reporting Services supports the following operating systems and platforms:

- Windows Server 2012
- Windows Server 2016
- Windows Server 2019

## SQL Server Reporting Services Features

The following is a list of features and configurations supported in Management Pack for SQL Server Reporting Services:

- SQL Server Reporting Services Instance (Native Mode)

- SQL Server Reporting Services Scale-out deployment

- Power BI Report Server - Verified with build 15.0.1107.165

  The management pack treats PBIRS as a special kind of SSRS and provides the same monitoring for PBIRS instances as it does for SSRS instances. In this guide, we will use SSRS or Reporting Services, but each term is intended for both SQL Server Reporting Services and Power BI Report Server.

## System Center Operations Manager

Management Pack for SQL Server Analysis Services supports the following versions of System Center Operations Manager:

- System Center Operations Manager 2012 R2
- System Center Operations Manager 2016
- System Center Operations Manager 1801
- System Center Operations Manager 1807
- System Center Operations Manager 2019

A dedicated Operations Manager management group is not required for this management pack.

