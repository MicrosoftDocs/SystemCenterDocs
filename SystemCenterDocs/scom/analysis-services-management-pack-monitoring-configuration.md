---
ms.assetid: 1c4927e5-5053-47e1-bf35-9aca5b4793a2
title: Monitoring configuration in Management Pack for SQL Server Analysis Services
description: This section explains monitoring configurations in Management Pack for SQL Server Analysis Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Configuration in Management Pack for SQL Server Analysis Services

This section explains monitoring configurations in Management Pack for SQL Server Analysis Services.

## Instance Monitoring

This scenario provides health monitoring of SSAS instances:

- **Service State**

    This monitor alerts when the Windows service for SSAS instance is not in the running state for a period longer than the specified threshold.

    >[!NOTE]
    > This monitor does not work on a clustered SSAS node.

- **Memory Configuration Conflict with SQL Server**

    This monitor alerts if there is a SQL Server relational database engine process running on the server and the **TotalMemoryLimit** configuration for a SSAS instance is higher than the specified threshold.

- **Total Memory Limit Configuration**

    This monitor alerts when configured **TotalMemoryLimit** for SSAS instance exceeds the specified threshold, risking allocation of physical memory required for the operating system to perform the necessary basic functions (at least 2 GB).

- **Memory Usage**

    This monitor reports a warning when memory allocations by SSAS instance surpasses the configured warning threshold expressed as a percentage of the **TotalMemoryLimit** setting for a SSAS instance. The monitor issues a critical alert when these allocations surpass the configured critical threshold.

- **Memory Usage on the Server**

    This monitor observes the memory usage by non-SSAS processes on the server to ensure that **TotalMemoryLimit** for Analysis Services is always available.

- **Processing Pool I/O Job Queue length**

    This monitor alerts when the length of the processing pool I/O job queue for SSAS instance is greater than the configured threshold.

- **Processing Pool Job Queue length**

    This monitor alerts when the length of the processing pool job queue for SSAS instance is greater than the configured threshold.

- **Query Pool Queue Length**

    This monitor alerts when the length of the query pool queue for SSAS instance is greater than the configured threshold.

- **Default Storage Free Space**

    This monitor reports a warning when the available free space for the instance default storage drops below Warning Threshold setting, expressed as a percentage of the sum of estimated default storage folder (DataDir) size and disk free space. The monitor reports a critical alert when the available space drops below Critical Threshold. The monitor does not take into account the databases or partitions located in folders other than the default storage folder (DataDir).

- **CPU utilization**

    This monitor alerts if the CPU usage by the SSAS process is high.

## Database Monitoring

This scenario provides health monitoring of SSAS Databases:

- **Database Free Space**

    This monitor reports a warning when the available disk space for SSAS database storage folder drops below Warning Threshold setting, expressed as a percentage of the sum of the estimated database storage folder size and disk free space. The monitor reports a critical alert when the available space drops below Critical Threshold.

- **Blocking Duration**

    This monitor alerts if at least one session is blocked longer than the configured threshold.

- **Blocking Session Count**

    This monitor alerts when the number of sessions blocked for a longer period than the configured WaitMinutes setting exceeds the configured threshold.

## Partition Monitoring

This scenario provides  monitoring for health aspects of SSAS Multidimensional Databases partitions:

- **Partition Storage Free Space**

    This monitor reports a warning when the available free space for the partition storage location drops below Critical Threshold setting expressed as a percentage of the sum of the total size of the folder plus disk free space.

    The monitor reports a critical alert when the available space drops below the Warning threshold. The monitor does not monitor available space for the default storage location for a SSAS instance.

- **Performance Collection Rules**

    This scenario collects various important performance metrics such as:

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