---
ms.assetid: 30b25bc3-54f4-484c-bf94-b397f44185f9
title: Security configuration in Management Pack for SQL Server Analysis Services
description: This article explains the security configuration in Management Pack for SQL Server Analysis Services
author: Anastas1ya
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Security Configuration in Management Pack for SQL Server Analysis Services

By default, all discoveries and monitors configured in [Management Pack for SQL Server](sql-server-management-pack-supported-configuration.md) use accounts defined in the **Default Action Account** Run As profile.

If the default action account for the given system doesn't have the necessary permissions to discover and monitor instances of SQL Server Analysis Services, those systems can be bound to more specific credentials in **Microsoft SQL Server** Run As profiles.

>[!NOTE]
>This management pack doesn't support least-privilege monitoring configurations and requires an action account to be a local administrator on SSAS servers.

## Default Run As Profiles

After importing the management pack, the following default Run As profiles are created:

- **Microsoft SQL Server Discovery Run As Profile**

    This profile is associated with discoveries:

    - Multidimensional DB
    - Multidimensional Instance
    - Multidimensional Partition
    - PowerPivot Instance
    - Tabular DB
    - Tabular Instance

- **Microsoft SQL Server Monitoring Run As Profile**

    This profile is associated with monitors and rules:

    - Monitors
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
    - Performance rules
        - Actual System Cache (GB)
        - Cache added KB/sec
        - Cache Evictions/sec
        - Cache Inserts/sec
        - Cleaner Current Price
        - CPU utilization (%)
        - Database Blocking Duration (minutes)
        - Database Blocking Duration (minutes)
        - Database Disk Free Space (GB)
        - Database Disk Free Space (%)
        - Database Drive Space Used By Others (GB)
        - Database Drive Space Used By Others (GB)
        - Database Free Space (%)
        - Database Free Space (%)
        - Database Free Space (GB)
        - Database Free Space (GB)
        - Database Size (GB)
        - Database Size (GB)
        - Database Storage Folder Size (GB)
        - Database Storage Folder Size (GB)
        - Default Storage Folder Size (GB)
        - Drive Used Space (GB)
        - Drive Used Space (GB)
        - Instance Free Space (%)
        - Instance Free Space (GB)
        - Instance Memory (%)
        - Instance Memory (GB)
        - Low Memory Limit (GB)
        - Memory Usage by AS Non-shrinkable (GB)
        - Memory Usage on the Server (%)
        - Memory Usage on the Server (GB)
        - Number of Database Blocked Sessions
        - Number of Database Blocked Sessions
        - Partition Free Space (%)
        - Partition Free Space (GB)
        - Partition Size (GB)
        - Partition Used by Others (GB)
        - Processing Pool I/O Job Queue Length
        - Processing Pool Job Queue Length
        - Processing Rows read/sec
        - Query Pool Job Queue Length
        - Storage Engine Query Rows sent/sec
        - Total Drive Size (GB)
        - Total Drive Size (GB)
        - Total Drive Size (GB)
        - Total Memory Limit (GB)
        - Total Memory on the Server (GB)
        - Used Space on Drive (GB)

## SQL Server and SQL Server Analysis Services Run As Profiles

To use separate accounts for monitoring of DB Engine, SSRS, and SSAS, create three different Windows accounts, and configure each account in each Run As profile according to the following table.

|Monitoring Account|[Association] Used for|
|-|-|
|SQL Server DB Monitoring Opt. # 1|**[Class]** SQL Server Components <br/> **[Class]** SQL Server DB Engine|
|SQL Server DB Monitoring Opt. # 2|**[Group]** SQL Server Components|
|SQL Server AS Monitoring|**[Class]** SSAS Seed <br/> **[Class]** SSAS Instance|
|SQL Server RS Monitoring|**[Class]** SSRS Deployment Seed <br/> **[Class]** Microsoft SQL Server Reporting Services Instance Seed <br/> **[Class]** Microsoft SQL Server Reporting Services (Native Mode) <br/> **[Class]** SSRS Deployment|

>[!NOTE]
>For the SQL Server DB account, use either **SQL Server DB Monitoring Opt. # 1** or **SQL Server DB Monitoring Opt. # 2**.
