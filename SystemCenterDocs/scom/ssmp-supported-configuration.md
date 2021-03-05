---
ms.assetid: 300c1177-469a-486e-8352-eea84cf8fdf8
title: Scope and Supported Configuration in Management Pack for SQL Server
description: This article explains the scope and supported configuration for Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for SQL Server

Management Pack for SQL Server is version-agnostic. It supports discovery and monitoring of SQL Server 2012 through 2019 and higher, including SQL on Linux with SQL Server 2017 and higher.

## Operating Systems and Platforms

Management Pack for SQL Server supports the following operating systems and platforms:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019
- Ubuntu 16.04 and 18.04
- Red Hat Enterprise Linux 7.3 and 7.4
- SUSE Linux Enterprise Server v12 SP2
- Docker Engine 1.8+
- Azure Kubernetes Service (AKS)

Localized versions of Windows Server are also supported.

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
  - Failover Clustering
  - Log Shipping
  - [Not supported] Replication

    Use dedicated management packs for SQL Server Replication to monitor this feature.
  
  - [Not supported] Mirroring
  - [Not supported] Domain-independent Availability Groups
  - [Not supported] Workgroup Cluster Availability Groups
- Authentication Mode — both SQL Server Authentication and Windows Authentication are supported.
- [Not supported] Localized versions of SQL Server

  Management Pack can only work with the English-language version of SQL Server.

- Express and Enterprise editions of SQL Server

## System Center Operations Manager

Management Pack for SQL Server supports the following versions of System Center Operations Manager:

- System Center Operations Manager 2012 R2
- System Center Operations Manager 2016
- System Center Operations Manager 1801
- System Center Operations Manager 1807
- System Center Operations Manager 2019

## Monitoring Modes

Management Pack for SQL Server supports the following monitoring modes:

- **Agent monitoring mode**
  
  Supported for SQL Server deployments on Windows.

- **Agentless monitoring mode**

  Supported for SQL Server deployments on both Windows and Linux.

- **Mixed monitoring mode**

  Supported for SQL Server deployments on Windows.
  
For more information about these modes, see [Monitoring Modes](ssmp-monitoring-modes.md).

## Management Groups

Management Pack for SQL Server does not require a dedicated Management Group and can work in virtual environments.