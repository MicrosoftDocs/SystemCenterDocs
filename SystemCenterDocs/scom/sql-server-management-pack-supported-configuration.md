---
ms.assetid: 300c1177-469a-486e-8352-eea84cf8fdf8
title: Scope and supported configuration in Management Pack for SQL Server
description: This article explains the scope and supported configuration for Management Pack for SQL Server
author: epomortseva
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 365-days
---

# Scope and Supported Configuration in Management Pack for SQL Server

## SQL Server Versions

::: moniker range="<=sc-om-2022"

Management Pack for SQL Server is version-agnostic. It supports the discovery and monitoring of SQL Server following versions:

- SQL Server 2012
  
  Due to the [Lifecycle Policy](/lifecycle/products/microsoft-sql-server-2012), this version is no longer being tested.

::: moniker-end

- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 (Windows and Linux platforms)
- SQL Server 2019 (Windows and Linux platforms)
- SQL Server 2022 (Windows and Linux platforms)

## SQL Server Features

Management Pack for SQL Server works with any edition of SQL Server from Express to Enterprise and supports the following features and configurations:

- SQL Server Database Engine
- SQL Server Database, including file groups, data files, transaction log files, FILESTREAM and Memory-Optimized Data containers.
- Different storage options for databases are supported:
  - Local storage (both drive letters and mount points)
  - Cluster Shared Volumes
  - SMB Shares
  - Azure BLOB
- SQL Server Agent and Jobs
- SQL Server Memory-Optimized Data (In-Memory OLTP)
- SQL Server High Availability Features:
  - Single-domain Availability Groups, including availability replicas and database replicas
  - Distributed Availability Groups
  - Contained Availability Groups
  - Failover Clustering
  - Log Shipping
  - [Not supported] Replication
  
    Use [dedicated management packs for SQL Server Replication](sql-replication-management-pack-changes-history.md) to monitor this feature.

  - [Not supported] Mirroring
  - [Not supported] Domain-independent Availability Groups
  - [Not supported] Workgroup Cluster Availability Groups
- Authentication Mode — both SQL Server Authentication and Windows Authentication are supported.
- Upgrade from a previous version of SQL Server
- [Not supported] Localized versions of SQL Server

  Management Pack for SQL Server supports English-language version of SQL Server only.

- [Not supported] 32-bit versions of SQL Server

>[!NOTE]
>Since Management Pack for SQL Server is unhosted, fully qualified domain names (FQDNs) are no longer displayed in System Center Operations Manager object names and alert properties.

## System Center Operations Manager

Management Pack for SQL Server supports the following versions of System Center Operations Manager:

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

## Operating Systems and Platforms

Management Pack for SQL Server supports the following operating systems and platforms:

::: moniker range="<=sc-om-2022"

- Windows Server 2012
  
  Due to the [Lifecycle Policy](/lifecycle/products/windows-server-2012), this version is no longer being tested.

- Windows Server 2012 R2
  
  Due to the [Lifecycle Policy](/lifecycle/products/windows-server-2012-r2), this version is no longer being tested.
  
- Windows Server 2016
- Windows Server 2019
- Windows Server 2022
::: moniker-end

::: moniker range="sc-om-2025"
- Windows Server 2019
- Windows Server 2022
- Windows Server 2025
::: moniker-end
- Ubuntu 16.04 - 22.04
- Red Hat Enterprise Linux 7.7 - 7.9, or 8.x - 9.x Server
- SUSE Linux Enterprise Server v12 - v15
- Docker Engine 1.8+
- Azure Kubernetes Service (AKS)

Localized versions of Windows Server are also supported.

## Monitoring Modes

Management Pack for SQL Server supports the following monitoring modes:

- **Agent monitoring mode**

  Supported for SQL Server deployments on Windows.

- **Agentless monitoring mode**

  Supported for SQL Server deployments on both Windows and Linux.

- **Mixed monitoring mode**

  Supported for SQL Server deployments on Windows.

For more information about these modes, see [Monitoring Modes](sql-server-management-pack-monitoring-modes.md).

## Management Groups

Management Pack for SQL Server does not require a dedicated Management Group and can work in virtual environments.
