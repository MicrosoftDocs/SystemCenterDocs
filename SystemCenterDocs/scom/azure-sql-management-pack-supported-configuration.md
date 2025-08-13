---
ms.assetid: 3b973a20-df14-490f-8452-020a9e3ede96
title: Scope and Supported Configuration in Management Pack for Azure SQL Database
description: This article explains the scope and supported configuration in Management Pack for Azure SQL Database
ms.custom: engagement-fy23
author: epomortseva
manager: evansma
ms.date: 04/23/2025
ms.author: jsuri
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Scope and Supported Configuration in Management Pack for Azure SQL Database

This article lists operating systems and features supported by Management Pack for Azure SQL Database.

Azure SQL Database is a fully managed Platform as a Service (PaaS) database engine that handles most of the database management functions such as upgrading, patching, backups, and monitoring without user involvement.

## Supported Azure SQL Database features and purchase models

Management Pack for Azure SQL Database supports the following Azure SQL Database features and configurations:

|Feature|Configurations|
|-|-|
|SQL Server|DTU metrics|
|SQL Database|  CPU metrics <br>DTU metrics <br>Connections metrics <br>Transactions metrics <br>Space metrics <br>Sessions metrics|
|SQL Elastic Pools|Storage metrics <br>DTU metrics <br>Sessions metrics <br>CPU metrics <br>I/O metrics|
|Database Geo-Replication|Geo-Replication Link State|


### Purchase Models

Management Pack for Azure SQL Database supports monitoring of databases in any of the following [purchase models](https://azure.microsoft.com/pricing/details/sql-database/single/):

|Model|Details|
|-|-|
|DTU-based SQL purchase models| Basic <br>Standard <br>Premium|
|vCore-based purchase models (**Provisioned** or **Serverless**)|General Purpose <br>Hyperscale <br>Business Critical|


When using the vCore-based purchase model, the following rules don't collect data because **DTULimit** metrics aren't available in this model:

- Azure SQL DB: DB DTU Used Count
- Azure SQL DB: DB DTU Limit Count
- Azure SQL DB: DB DTU Percentage

## System Center Operations Manager

Management Pack for Azure SQL Database supports the following versions of System Center Operations Manager:

::: moniker range="<=sc-om-2022"

- System Center Operations Manager 2012 R2
  
  Due to the [Lifecycle Policy](/lifecycle/products/microsoft-system-center-2012-r2-operations-manager), this version is no longer being tested.
  
- System Center Operations Manager 2016
- System Center Operations Manager 2019
- System Center Operations Manager 2022
::: moniker-end

::: moniker range="sc-om-2025"

- System Center Operations Manager 2019
- System Center Operations Manager 2022
- System Center Operations Manager 2025
::: moniker-end

>[!NOTE]
> To connect System Center Operations Manager to Azure resources, your server must have TLS 1.2 enabled. Check protocol status with [TLS 1.2 enforcement for Azure AD Connect](/azure/active-directory/hybrid/reference-connect-tls-enforcement#powershell-script-to-check-tls-12).
## Operating Systems and Platforms

Management Pack for Azure SQL Database supports the following 64-bit operating systems and platforms:

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
