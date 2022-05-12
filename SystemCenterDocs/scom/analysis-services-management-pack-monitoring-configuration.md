---
ms.assetid: 1c4927e5-5053-47e1-bf35-9aca5b4793a2
title: Monitoring configuration in Management Pack for SQL Server Analysis Services
description: This section explains monitoring configurations in Management Pack for SQL Server Analysis Services
author: TDzakhov
manager: evansma
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Configuration in Management Pack for SQL Server Analysis Services

This section explains monitoring configurations in Management Pack for SQL Server Analysis Services.

## Instance Monitoring

The following monitors are available for monitoring of SSAS instances.

|Monitor|Description
|-|-|
|Service State|This monitor reports an alert when the Windows service for the SSAS instance is not in the running state for a period that exceeds the specified threshold. <br /> <br /> **NOTE:** This monitor does not work on a clustered SSAS instance.|
|Memory Configuration Conflict with SQL Server|This monitor reports an alert if there is a SQL Server relational database engine process running on the server and the **TotalMemoryLimit** configuration for the SSAS instance is higher than the specified threshold.|
|Total Memory Limit Configuration|This monitor reports an alert when the configured **TotalMemoryLimit** setting for the SSAS instance exceeds the specified threshold, risking allocation of physical memory that is required for the operating system to perform basic functions (at least 2 GB).|
|Memory Usage| This monitor reports a Warning alert when memory allocations by the SSAS instance exceeds the configured warning threshold expressed as a percentage of the **TotalMemoryLimit** setting for the SSAS instance. The monitor reports a Critical alert when these allocations exceed the configured critical threshold.|
|Memory Usage on the Server|This monitor observes the memory usage by non-SSAS processes on the server to ensure that **TotalMemoryLimit** for Analysis Services is always available.|
|Processing Pool I/O Job Queue length|This monitor reports an alert when the processing pool I/O job queue for the SSAS instance exceeds the configured threshold.|
|Processing Pool Job Queue length|This monitor reports an alert when the processing pool job queue for the SSAS instance exceeds the configured threshold.|
|Default Storage Free Space|This monitor reports a Warning alert when the available free space for the instance default storage drops below the **Warning Threshold** setting expressed as a percentage of the sum of estimated default storage folder (DataDir) size and free disk space. The monitor reports a Critical alert when the available space drops below **Critical Threshold**. The monitor does not take into account databases and partitions located in folders other than the default storage folder (DataDir).|
|CPU utilization|This monitor reports an alert if the CPU usage by the SSAS process is high.|

## Database Monitoring

The following monitors are available for monitoring of SSAS databases.

|Monitor|Description
|-|-|
|Database Free Space|This monitor reports a Warning alert when the available disk space for the SSAS database storage folder drops below the **Warning Threshold** setting expressed as a percentage of the sum of the estimated database storage folder size and disk free space. The monitor reports a Critical alert when the available space drops below the **Critical Threshold** setting.|
|Blocking Duration|This monitor report an alert if at least one session is blocked longer than the configured threshold.|
|Blocking Session Count|This monitor alerts when the number of sessions that are blocked for a period longer than the **WaitMinutes** setting exceeds the threshold.|

## Partition Monitoring

The following monitors are available for monitoring of health aspects of SSAS Multidimensional Databases partitions.

|Monitor|Description
|-|-|
|Partition Storage Free Space|This monitor reports a Warning alert when the available free space for the partition storage location drops below the **Critical Threshold** setting expressed as a percentage of the sum of the total size of the folder plus disk free space. The monitor reports a Critical alert when the available space drops below the Warning threshold. The monitor does not monitor available space for the default storage location for the SSAS instance.|

### Performance Collection Rules

Performance collection rules collect the following metrics:

- SSAS: Database Disk Free Space (GB)
- SSAS: Database Drive Space Used By Others (GB)
- SSAS: Database Blocking Duration (minutes)
- SSAS: Database Free Space (%)
- SSAS: Database Free Space (GB)
- SSAS: Number of Database Blocked Sessions
- SSAS: Database Size (GB)
- SSAS: Database Storage Folder Size (GB)
- SSAS: Partition Size (GB)
- SSAS: Partition Free Space (GB)
- SSAS: Partition Used by Others (GB)
- SSAS: Partition Free Space (%)
- SSAS: Total Drive Size (GB)
- SSAS: Drive Used Space (GB)
- SSAS: Actual System Cache (GB)
- SSAS: Instance Free Space (%)
- SSAS: Instance Free Space (GB)
- SSAS: Cache Evictions/sec
- SSAS: Cache Inserts/sec
- SSAS: Cache KB added/sec
- SSAS: CPU utilization (%)
- SSAS: Default Storage Folder Size (GB)
- SSAS: Low Memory Limit (GB)
- SSAS: Cleaner Current Price
- SSAS: Memory Usage on the Server (GB)
- SSAS: Memory Usage on the Server (%)
- SSAS: Memory Usage by AS Non-shrinkable (GB)
- SSAS: Processing Pool I/O Job Queue Length
- SSAS: Processing Pool Job Queue Length
- SSAS: Processing Rows read/sec
- SSAS: Instance Memory (GB)
- SSAS: Instance Memory (%)
- SSAS: Query Pool Job Queue Length
- SSAS: Storage Engine Query Rows sent/sec
- SSAS: Total Memory Limit (GB)
- SSAS: Total Memory on the Server (GB)
- SSAS: Used Space on Drive (GB)

## How Health Rolls Up

The following diagram shows the roll up of the object health states.

![Health Rolls Up](./media/analysis-services-management-pack/health-rolls-up.png)
