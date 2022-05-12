---
ms.assetid: 3b973a20-df14-490f-8452-020a9e3ede96
title: Scope and supported configuration in Management Pack for Azure SQL Database
description: This article explains the scope and supported configuration in Management Pack for Azure SQL Database
author: TDzakhov
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for Azure SQL Database

This section lists operating systems and features supported by Management Pack for Azure SQL Database.

Azure SQL Database is a fully managed platform as a service (PaaS) database engine that handles most of the database management functions such as upgrading, patching, backups, and monitoring without user involvement.

## Operating Systems

Management Pack for Azure SQL Database supports the following operating systems:

  - Windows Server 2012
  - Windows Server 2012 R2
  - Windows Server 2016
  - Windows Server 2019

## Supported Azure SQL Database Features and Purchase Models

Management Pack for Azure SQL Database supports the following Azure SQL Database features and configurations:

- SQL Server
  - DTU metrics
- SQL Database
  - CPU metrics
  - DTU metrics
  - Connections metrics
  - Transactions metrics
  - Space metrics
  - Sessions metrics
- SQL Elastic Pools
  - Storage metrics
  - DTU metrics
  - Sessions metrics
  - CPU metrics
  - I/O metrics
- Database Geo-Replication
  - Geo-Replication Link State

### Purchase Models

Management Pack for Azure SQL Database supports monitoring of databases in any of the following [purchase models](https://azure.microsoft.com/pricing/details/sql-database/single/):

- DTU-based SQL purchase models
  - Basic
  - Standard
  - Premium

- vCore-based purchase models (**Provisioned** or **Serverless**)
  - General Purpose
  - Hyperscale
  - Business Critical

When using the vCore-based purchase model, the following rules do not collect data because **DTULimit** metrics are not available in this model:

- Azure SQL DB: DB DTU Used Count
- Azure SQL DB: DB DTU Limit Count
- Azure SQL DB: DB DTU Percentage

>[!NOTE]
>When using the Hyperscale service tier, some of the space monitoring workflows may not collect data correctly. For more information see the related [Known Issue](azure-sql-management-pack-known-issues-and-troubleshooting.md).

## System Center Operations Manager

Management Pack for Azure SQL Database supports the following versions of System Center Operations Manager:

  - System Center Operations Manager 2012 R2
  - System Center Operations Manager 2016
  - System Center Operations Manager 1801
  - System Center Operations Manager 1807
  - System Center Operations Manager 2019
