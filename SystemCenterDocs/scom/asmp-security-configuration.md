---
ms.assetid: 30b25bc3-54f4-484c-bf94-b397f44185f9
title: Security Configuration in Management Pack for SQL Server Analysis Services
description: This article explains the monitoring configuration in Management Pack for SQL Server Analysis Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Security Configuration in Management Pack for SQL Server Analysis Services

This management pack does not support least-privilege monitoring configurations and requires an action account to be a local administrator on the SSAS servers.

By default, all discoveries and monitors configured in [Management Pack for SQL Server](ssmp-supported-configuration.md) use accounts defined in the **Default Action Account** Run As profile.

If the default action account for the given system does not have necessary permissions to discover and monitor instances of SQL Server Analysis Services, those systems can be bound to more specific credentials in **Microsoft SQL Server** Run As profiles.

## Run As Profiles

After importing the management pack, the following default Run As profiles are created:

- **Microsoft SQL Server Discovery Run As Profile**

    This profile is associated with discoveries:

    - MSSQL Analysis Services: Multidimensional DB Discovery
    - MSSQL Analysis Services: Multidimensional Instance Discovery
    - MSSQL Analysis Services: Multidimensional Partition Discovery
    - MSSQL Analysis Services: PowerPivot Instance Discovery
    - MSSQL Analysis Services: Tabular DB Discovery
    - MSSQL Analysis Services: Tabular Instance Discovery

- **Microsoft SQL Server Monitoring Run As Profile**

    This profile is associated with monitors and rules:

    - Blocking Duration
    - Blocking Session Count
    - CPU Utilization (%)
    - Database Free Space
    - Default Storage Free Space
    - Memory Configuration
    - Conflict with SQL Server Memory Usage
    - Memory Usage on the Server
    - Partition Storage Free Space
    - Processing Pool I/O Job Queue length
    - Processing Pool Job Queue length
    - Query Pool Queue length
    - Service State
    - Total Memory Limit Configuration
    - Database Status
    - SSAS: Actual System Cache (GB)
    - SSAS: Cache added KB/sec
    - SSAS: Cache Evictions/sec
    - SSAS: Cache Inserts/sec
    - SSAS: Cleaner Current Price
    - SSAS: CPU utilization (%)
    - SSAS: Database Blocking Duration (minutes)
    - SSAS: Database Blocking Duration (minutes)
    - SSAS: Database Disk Free Space (GB)
    - SSAS: Database Disk Free Space (%)
    - SSAS: Database Drive Space Used By Others (GB)
    - SSAS: Database Drive Space Used By Others (GB)
    - SSAS: Database Free Space (%)
    - SSAS: Database Free Space (%)
    - SSAS: Database Free Space (GB)
    - SSAS: Database Free Space (GB)
    - SSAS: Database Size (GB)
    - SSAS: Database Size (GB)
    - SSAS: Database Storage Folder Size (GB)
    - SSAS: Database Storage Folder Size (GB)
    - SSAS: Default Storage Folder Size (GB)
    - SSAS: Drive Used Space (GB)
    - SSAS: Drive Used Space (GB)
    - SSAS: Instance Free Space (%)
    - SSAS: Instance Free Space (GB)
    - SSAS: Instance Memory (%)
    - SSAS: Instance Memory (GB)
    - SSAS: Low Memory Limit (GB)
    - SSAS: Memory Usage by AS Non-shrinkable (GB)
    - SSAS: Memory Usage on the Server (%)
    - SSAS: Memory Usage on the Server (GB)
    - SSAS: Number of Database Blocked Sessions
    - SSAS: Number of Database Blocked Sessions
    - SSAS: Partition Free Space (%)
    - SSAS: Partition Free Space (GB)
    - SSAS: Partition Size (GB)
    - SSAS: Partition Used by Others (GB)
    - SSAS: Processing Pool I/O Job Queue Length
    - SSAS: Processing Pool Job Queue Length
    - SSAS: Processing Rows read/sec
    - SSAS: Query Pool Job Queue Length
    - SSAS: Storage Engine Query Rows sent/sec
    - SSAS: Total Drive Size (GB)
    - SSAS: Total Drive Size (GB)
    - SSAS: Total Drive Size (GB)
    - SSAS: Total Memory Limit (GB)
    - SSAS: Total Memory on the Server (GB)
    - SSAS: Used Space on Drive (GB)
