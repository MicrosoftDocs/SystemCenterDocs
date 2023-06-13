---
ms.assetid: 1c4927e5-5053-47e1-bf35-9aca5b4793a2
title: Monitoring configuration in Management Pack for SQL Server Analysis Services
description: This article explains monitoring configurations in Management Pack for SQL Server Analysis Services
manager: evansma
author: epomortseva
ms.author: v-ekaterinap
ms.date: 06/13/2023
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Configuration in Management Pack for SQL Server Analysis Services

A server instance of Analysis Services is a copy of the msmdsrv.exe executable that runs as an operating system service. Each instance is fully independent of other instances on the same server, having its own configuration settings, permissions, ports, startup accounts, file storage, and server mode properties.

Management Pack for SQL Server Analysis Services automatically discovers instances of SQL Server Analysis Services by implementing the following workflows:

- Reading the registry to detect if SQL Server Analysis Services is installed on the server. If installed, the management pack creates a seed object.

- If the seed object is discovered, the management pack reads such data sources as the registry, WMI, SQL Server Analysis Services configuration file, and so on, to discover instance properties and the **Seed** object.

## Discovery of SQL Server Analysis Services Instance

Analysis Services Instance includes the following server modes:

- Multidimensional mode
- Tabular mode
- Power Pivot for SharePoint mode

For comparing model features, see the [determine the Server Mode of an Analysis Services Instance](/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance) article.

## Discovery of SQL Server Analysis Services Database

Analysis Services Database includes the following server modes:

- Multidimensional Database
  - Partition
- Tabular Database

## Disabling Monitoring of Specified SQL Server Analysis Services Versions

Management Pack for SQL Server Analysis Services allows you to exclude certain versions of SQL Server Analysis Services from monitoring.

To exclude versions that you don't want to monitor, override the **Versions of SQL Server to be excluded** parameter in the **SSAS: Multidimensional Instance Discovery**, **SSAS: PowerPivot Instance Discovery**, or **SSAS: Tabular Instance Discovery** discovery with the versions that you want to exclude. Use commas to specify multiple versions.

For example, an override "2014,2016" instructs the management pack to skip instances of SQL Server Analysis Services 2014 and 2016.

![Screenshot of disabling Monitoring of Specified SQL Server Versions.](./media/analysis-services-management-pack/overriding-version-parameter.png)

## Disabling Monitoring of Specified SQL Server Analysis Services Editions

Management Pack for SQL Server Analysis Services allows you to exclude certain editions of SQL Server Analysis Services instances from monitoring.

To exclude editions that you don't want to monitor, override the **Editions of SQL Server to be excluded** parameter in the **SSAS: Multidimensional Instance Discovery**, **SSAS: PowerPivot Instance Discovery**, or **SSAS: Tabular Instance Discovery** discovery with the editions that you want to exclude. Use commas to specify multiple editions.

The following table lists short names that you can use to override the **Editions of SQL Server to be excluded** parameter.

|Short Name|Covered Editions|
|-|-|
|Enterprise|Enterprise Edition, Enterprise Edition: Core-based Licensing|
|Standard|Standard Edition, Business Intelligence Edition|
|Web|Web Edition|
|Developer|Developer Edition|
|Express|Express Edition, Express Edition with Advanced Services|
|Evaluation|Enterprise Evaluation Edition|

![Screenshot of disabling Monitoring of Specified SQL Server Editions.](./media/analysis-services-management-pack/overriding-edition-parameter.png)

## Disabling Monitoring of Specified Databases by Name

You can disable discovery and monitoring of databases by specifying database names in the **Exclude list** parameter available in the following discoveries:

- Multidimensional DB Discovery

- Tabular DB Discovery

Use commas to separate database names and asterisks to replace one or more characters. For example, when setting the **Exclude list** parameter to dev*, \*test*, *stage, dbnotmon, the monitoring behavior would be as follows:

|DB Name|Monitored/Not monitored|
|-|-|
|dev|Not monitored|
|dev_sales|Not monitored|
|sales_dev|Monitored|
|test|Not monitored|
|test_sales|Not monitored|
|sales_test|Not monitored|
|stage|Not monitored|
|stage_dev|Monitored|
|dev_stage|Not monitored|
|dbnotmon|Not monitored|
|dbnotmon_sales|Monitored|
|sales_dbnotmon|Monitored|

If you've \* (asterisk) in the list as a database name (for example, \*temp*, \*, \*dev* or \*temp,*), it disables the monitoring of any database.

## Instance Monitoring

The following monitors are available for the monitoring of SQL Server Analysis Services instances.

|Monitor|Description
|-|-|
|Service State|This monitor reports an alert when the Windows service for the SQL Server Analysis Services instance isn't in the running state for a period that exceeds the specified threshold. <br /> <br /> **NOTE:** This monitor doesn't work on a clustered SQL Server Analysis Services instance.|
|Memory Configuration Conflict with SQL Server|This monitor reports an alert if there's a SQL Server relational database engine process running on the server, and the **TotalMemoryLimit** configuration for the SQL Server Analysis Services instance is higher than the specified threshold.|
|Total Memory Limit Configuration|This monitor reports an alert when the configured **TotalMemoryLimit** setting for the SQL Server Analysis Services instance exceeds the specified threshold, risking allocation of physical memory that is required for the operating system to perform basic functions (at least 2 GB).|
|Memory Usage| This monitor reports a Warning alert when memory allocations by the SQL Server Analysis Services instance exceed the configured warning threshold expressed as a percentage of the **TotalMemoryLimit** setting for the SQL Server Analysis Services instance. The monitor reports a Critical alert when these allocations exceed the configured critical threshold.|
|Memory Usage on the Server|This monitor observes the memory usage by non-SSAS processes on the server to ensure that **TotalMemoryLimit** for Analysis Services is always available.|
|Processing Pool I/O Job Queue length|This monitor reports an alert when the processing pool I/O job queue for the SQL Server Analysis Services instance exceeds the configured threshold.|
|Processing Pool Job Queue length|This monitor reports an alert when the processing pool job queue for the SQL Server Analysis Services instance exceeds the configured threshold.|
|Default Storage Free Space|This monitor reports a Warning alert when the available free space for the instance default storage drops below the **Warning Threshold** setting expressed as a percentage of the sum of estimated default storage folder (DataDir) size and free disk space. The monitor reports a Critical alert when the available space drops below **Critical Threshold**. The monitor doesn't take into account databases and partitions located in folders other than the default storage folder (DataDir).|
|CPU utilization|This monitor reports an alert if the CPU usage by the SQL Server Analysis Services process is high.|

## Database Monitoring

The following monitors are available for monitoring of SQL Server Analysis Services databases.

|Monitor|Description
|-|-|
|Database Status|This monitor checks the status of the Microsoft SQL Server Analysis Services database. Status check is done by running a query against the SQL Server Analysis Services instance database which returns the current database state.
|Database Free Space|This monitor reports a Warning alert when the available disk space for the SQL Server Analysis Services database storage folder drops below the **Warning Threshold** setting expressed as a percentage of the sum of the estimated database storage folder size and disk free space. The monitor reports a Critical alert when the available space drops below the **Critical Threshold** setting.|
|Blocking Duration|This monitor report an alert if at least one session is blocked longer than the configured threshold.|
|Blocking Session Count|This monitor alerts when the number of sessions that are blocked for a period longer than the **WaitMinutes** setting exceeds the threshold.|
|Database VertiPaq Size|This monitor reports a warning when the amount of VertiPaq memory consumed by SQL Server Analysis Services tabular databases exceeds the 'Warning Threshold' override (specified in GB). In cases when tabular databases consume more VertiPaq memory than it's allowed by the 'Critical Threshold' override, the monitor throws a critical alert.|

## Partition Monitoring

The following monitors are available for monitoring of health aspects of SQL Server Analysis Services Multidimensional Databases partitions.

|Monitor|Description
|-|-|
|Partition Storage Free Space|This monitor reports a Warning alert when the available free space for the partition storage location drops below the **Critical Threshold** setting expressed as a percentage of the sum of the total size of the folder plus disk free space. The monitor reports a Critical alert when the available space drops below the Warning threshold. The monitor doesn't monitor available space for the default storage location for the SQL Server Analysis Services instance.|

## Performance Collection Rules

Performance collection rules collect the following metrics:

- Database Disk Free Space (GB)
- Database Drive Space Used By Others (GB)
- Database Blocking Duration (minutes)
- Database Free Space (%)
- Database Free Space (GB)
- Number of Database Blocked Sessions
- Database Size (GB)
- Database Storage Folder Size (GB)
- Partition Size (GB)
- Partition Free Space (GB)
- Partition Used by Others (GB)
- Partition Free Space (%)
- Total Drive Size (GB)
- Drive Used Space (GB)
- Actual System Cache (GB)
- Instance Free Space (%)
- Instance Free Space (GB)
- Cache Evictions/sec
- Cache Inserts/sec
- Cache KB added/sec
- CPU utilization (%)
- Default Storage Folder Size (GB)
- Low Memory Limit (GB)
- Cleaner Current Price
- Memory Usage on the Server (GB)
- Memory Usage on the Server (%)
- Memory Usage by AS Non-shrinkable (GB)
- Processing Pool I/O Job Queue Length
- Processing Pool Job Queue Length
- Processing Rows read/sec
- Instance Memory (GB)
- Instance Memory (%)
- Query Pool Job Queue Length
- Storage Engine Query Rows sent/sec
- Total Memory Limit (GB)
- Total Memory on the Server (GB)
- Used Space on Drive (GB)
- Database VertiPaq Memory Size (GB)

## Tasks Overview

The SQL Server Analysis Services Management Pack provides tasks for some activities with the target Instance:

- **Export Event Log**

   Export the Windows Event log file from the the machine hosting SQL Server Analysis Services instance.
   The exported source events with ID 4221 are:

  - SQL Server Analysis Services MP Library
  - SQL Server Analysis Services Discovery MP
  - SQL Server Analysis Services Monitoring MP
  - SQL Server MP Default

   For more information, see [Export Event Log Task](sql-server-management-pack-export-event-log-task.md).

- **Start Analysis Services**

    SQL Server Analysis Services instance can be started by task from System Center Operations Manager.

- **Stop Analysis Services**

    SQL Server Analysis Services instance can be stopped by task from System Center Operations Manager.

## Enabling Debugging

In Management Pack for SQL Server Analysis Services, you can enable debugging in the Windows Event log in cases when you want to investigate potential issues that may occur during monitoring or see the detailed data sets used in the management pack workflows.

To enable debugging, do the following:

1. Open the Windows registry.

2. Create the following key:
`HKLM:\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\SQL Management Packs\EnableEvtLogDebugOutput\SQL Server Analysis Services MP`

3. Create a Multi-String with the name `<MG Name>` that corresponds to the management group name for which you want to collect logs. Leave **Value data** empty to enable Debug logging for all SQL MP modules in the Operations Manager Event Log.

Or use the following PowerShell script to enable debugging in automated mode:

```PowerShell
$SCOMRoot = 'HKLM:\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\'
$MPDebugKey = Join-Path -Path $SCOMRoot -ChildPath 'SQL Management Packs\EnableEvtLogDebugOutput\SQL Server Analysis Services MP'
$AgRoot = Join-Path -Path $SCOMRoot -ChildPath 'Agent Management Groups'
$SrvRoot = Join-Path -Path $SCOMRoot -ChildPath 'Server Management Groups'
$searchPath = if (Test-Path $AgRoot) { $AgRoot } else { $SrvRoot }

if (-not(Test-Path $SCOMRoot)) {
    Write-Error 'The Microsoft Operations Manager or Monitoring Agent is not installed.' -ErrorAction Stop
}

if (-not(Test-Path $MPDebugKey)) {
    New-Item -Path $MPDebugKey -Force | Out-Null
}

Get-ChildItem -Path $searchPath |
Out-GridView -OutputMode Multiple | # Remove this line if there's no need for GUI
ForEach-Object {
    New-ItemProperty -LiteralPath $MPDebugKey -Name $_.PSChildName -Value '1' -PropertyType 'MultiString' -Force | Out-Null
}
```

The same should be done for each Operations Manager or Monitoring Agent where extended logging must be enabled. You don't need to restart any service; changes are applied automatically.

## Disabling Debugging

To disable debugging, delete the keys added above or use the following PowerShell script to disable debugging in automated mode:

```PowerShell
$MPDebugKey = 'HKLM:\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\SQL Management Packs\EnableEvtLogDebugOutput\SQL Server Analysis Services MP'

if (-not(Test-Path $MPDebugKey)) {
    Write-Error 'The Microsoft Operations Manager or Monitoring Agent is not installed.' -ErrorAction Stop
}

(Get-Item -Path $MPDebugKey).property |
Out-GridView -OutputMode Multiple | # Remove this line if there is no need for GUI
ForEach-Object {
    Remove-ItemProperty -LiteralPath $MPDebugKey -Name $_ -Force | Out-Null
}
```

> [!NOTE]
> Currently, you can enable extended logging for all SQL MP modules only. Extended logging of separate modules isn't supported yet.

## How Health Rolls Up

The following diagram shows the rollup of the object health states.

![Diagram of health Rolls Up.](./media/analysis-services-management-pack/health-rolls-up.png)
