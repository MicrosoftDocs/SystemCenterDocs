---
ms.assetid: 5a3a8b98-1113-45bf-9484-2c807ec3d013
title: SQL Server Design Considerations
description: This article provides detailed design guidance for SQL Server to support the Operations Manager databases and reporting component.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.custom: engagement-fy23, UpdateFrequency.5
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# SQL Server Design Considerations

System Center Operations Manager relies on Microsoft SQL Server to support its operational, data warehouse, and ACS audit databases. These databases are essential and are created during the deployment of the first management server or ACS collector in your management group.

In a lab environment or small-scale deployment of Operations Manager, SQL Server can be colocated on the first management server in the management group.

In a medium to enterprise-scale distributed deployment, the SQL Server instance should be located on a dedicated standalone server or in a SQL Server high-availability configuration. In either case, SQL Server must already exist and is accessible before you start the installation of the first management server or ACS collector.

We don't recommend utilization of Operations Manager databases from a SQL Instance that has other application databases to avoid any potential issues with I/O and other hardware resource restrictions.

> [!IMPORTANT]
> Operations Manager does not support Platform as a Service (PaaS) instances of SQL, including products such as Azure SQL Managed Instance or Amazon Relational Database Service (AWS RDS). Please use an instance of SQL Server installed on a Windows machine. The only exception to this is within [Azure Monitor SCOM Managed Instance](./operations-manager-managed-instance-overview.md), which utilizes Azure SQL MI, and is not reconfigurable.

## SQL Server requirements

The following versions of SQL Server Enterprise & Standard Edition are supported for an existing installation of System Center Operations Manager version to host Reporting Server, Operational, Data Warehouse, and ACS database:

::: moniker range="sc-om-2019"

- SQL Server 2019 with a **minimum Cumulative Update 8 (CU8)** or later update as available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2019)
- SQL Server 2016 and the latest updates available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2016)

::: moniker-end

::: moniker range=">=sc-om-2022"

- SQL Server 2022 with a **minimum Cumulative Update 11 (CU11)** or later update as available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2022)
- SQL Server 2019 with a **minimum Cumulative Update 8 (CU8)** or later update as available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2019)
- SQL Server 2017 with the latest available update as available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2017)

::: moniker-end


::: moniker range="sc-om-2019"

- SQL Server 2017 and Cumulative Updates as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)
- SQL Server 2016 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)

::: moniker-end

::: moniker range=">=sc-om-2019"

Before upgrading SQL Server, see [upgrade information for 2017+](upgrade-sqlserver-2017-opsmgr.md) and [upgrade information for SQL 2019](upgrade-sqlserver-2019-operations-manager.md).

::: moniker-end

::: moniker range="sc-om-2016"
The following versions of SQL Server Enterprise & Standard Edition are supported for a new or existing installation of System Center 2016 - Operations Manager to host Reporting Server, Operational, Data Warehouse, and ACS database:

- SQL Server 2016 and the latest updates available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2016)
- SQL Server 2014 and the latest updates available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2014)
- SQL Server 2012 and the latest updates available [here](/troubleshoot/sql/releases/download-and-install-latest-updates#sql-server-2012)

::: moniker-end

### SQL Server drivers

The [OLE DB](/sql/connect/oledb/oledb-driver-for-sql-server) and [ODBC](/sql/connect/odbc/microsoft-odbc-driver-for-sql-server) SQL Server Drivers need to be installed on **all** management servers and the web console server, as these components directly interface with the databases and these drivers allow API level access to SQL.

It is recommended to utilize an encrypted SQL Server connection; when doing so, you need to install the latest versions of the SQL drivers:

- [Microsoft OLE DB Driver](https://aka.ms/downloadmsoledbsql) latest version.
- [Microsoft ODBC Driver](https://aka.ms/downloadmsodbcsql) latest version.

More information about configuring SQL connection encryption can be found here: [Configure SQL Server Database Engine for encrypting connections](/sql/database-engine/configure-windows/configure-sql-server-encryption)

If **not** utilizing encrypted SQL connections, use previous releases of the SQL drivers that do not enforce encryption:

- [Microsoft ODBC Driver](/sql/connect/odbc/windows/release-notes-odbc-sql-server-windows?view=sql-server-ver16#17106) version 17.10.6.
- [Microsoft OLE DB Driver](/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-ver16#1874) version 18.7.4.

### SQL Server updates

 Each of the following SQL Server components supporting an Operations Manager infrastructure are required to be at the same SQL Server major version:

- SQL Server database engine instances hosting any of the Operations Manager databases, including:
  - OperationManager
  - OperationManagerDW
  - SSRS databases ReportServer and ReportServerTempDB
- SQL Server Reporting Services (SSRS) instance.

### SQL Server authentication mode

By default, SQL operates in a Mixed Mode authentication configuration. However, Operations Manager only utilizes Windows authentication to communicate with SQL Server. If left at default, SQL Mixed Mode Authentication setting will still work if no local account has the `db_owner` role. Local accounts with the `db_owner` role are known to cause issues with Operations Manager.

It's highly recommended to remove the `db_owner` role from all the local accounts before installing the product and don’t add the `db_owner` role to any local accounts after installation.

### Other considerations

Other hardware and software considerations apply in your design planning:

- IT is recommended to have SQL disks in NTFS file format.
- You must have at least 1 GB of free disk space for the operational and data warehouse database, this is enforced at the time of database creation. Keep in mind that the disk utilization of **the databases will grow significantly after setup**, ensure to have plenty of free disk space above this base requirement.
- .NET Framework 4 is required.
- .NET Framework 4.8 is supported from Operations Manager 2022.
- Reporting Server isn't supported on Windows Server Core.
- The SQL Server collation setting must be one of the supported types as described in the section: [**SQL Server collation setting**](#sql-server-collation-setting).
- SQL Server Full Text Search is required for all SQL Server database engine instances hosting any of the Operations Manager databases.
- The Windows Server installation options (Server Core, Server with Desktop Experience, and Nano Server) supported by Operations Manager database components are based on what installation options are supported by SQL Server.

For more information, see the Hardware & Software Requirements section under the SQL Server installation and planning documentation here: [Plan a SQL Server installation](/sql/sql-server/install/planning-a-sql-server-installation)

## SQL Server collation setting

The following SQL Server and Windows collations are supported in System Center Operations Manager.

> [!NOTE]
> To avoid any compatibility issues in comparing or copying operations, we recommend you use the same collation for the SQL and Operations Manager DB.

### SQL Server collation

- SQL_Latin1_General_CP1_CI_AS

### Windows collation

- Latin1_General_100_CI_AS
- French_CI_AS
- French_100_CI_AS
- Cyrillic_General_CI_AS
- Chinese_PRC_CI_AS
- Chinese_Simplified_Pinyin_100_CI_AS
- Chinese_Traditional_Stroke_Count_100_CI_AS
- Japanese_CI_AS
- Japanese_XJIS_100_CI_AS
- Traditional_Spanish_CI_AS
- Modern_Spanish_100_CI_AS
- Latin1_General_CI_AS
- Cyrillic_General_100_CI_AS
- Korean_100_CI_AS
- Czech_100_CI_AS
- Hungarian_100_CI_AS
- Polish_100_CI_AS
- Finnish_Swedish_100_CI_AS  

If your SQL Server instance isn't configured with one of the supported collations listed earlier, performing a new setup of Operations Manager setup fails. However, an in-place upgrade completes successfully.

## Firewall configuration

Operations Manager depends on SQL Server to host its databases and a reporting platform to analyze and present historical operational data. The management server, Operations, and Web console roles need to be able to successfully communicate with SQL Server, and it's important to understand the communication path and ports in order to configure your environment correctly.

If designing a distributed deployment that using SQL Always On Availability Groups, there are extra firewall configuration settings that need to be included in your firewall security strategy.

The following table identifies the firewall ports required by SQL Server in order for management servers to communicate with the databases:

| Scenario | Port | Direction | Operations Manager Role |
|-----------|---------------|---------------|---------------|
| SQL Server hosting Operations Manager databases | TCP 1433 \* | Inbound | management server and Web console (for Application Advisor and Application Diagnostics) |
| SQL Server Browser service | UDP 1434 | Inbound | management server |
| SQL Server Dedicated Admin Connection | TCP 1434 | Inbound | management server |
| Other ports used by SQL Server<br> - Microsoft remote procedure calls (MS RPC)<br> - Windows Management Instrumentation (WMI)<br> - Microsoft Distributed Transaction Coordinator (MS DTC)| TCP 135 | Inbound | management server |
| SQL Server Always On Availability Group Listener | Administrator configured port | Inbound | management server
| SQL Server Reporting Services hosting Operations Manager Reporting Server | TCP 80 (default)/443 (SSL) | Inbound | management server and Operations console |  

> [!NOTE]
> While TCP 1433 is the standard port for the default instance of the Database Engine, when you create a named instance on a standalone SQL Server or have deployed a SQL Always On Availability Group, a custom port is defined and should be documented for reference so that you properly configure your firewalls and enter this information during setup.

For a more detailed overview of the firewall requirements for SQL Server, see [Configure the Windows Firewall to Allow SQL Server Access](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).

## Capacity and storage considerations

### Operations Manager database

The Operations Manager database is a SQL Server database that contains all of the data needed by Operations Manager for day-to-day monitoring. Sizing and configuration of the database server is critical to the overall performance of the management group. The most critical resource used by the Operations Manager database is the storage subsystem, but CPU and RAM are also significant.

Factors that influence the load on the Operations Manager database include:

- Rate of operational data collection.
  - The rate of operational data collection is influenced by factors such as the number of management packs imported, the number of agents added, and the type of computer being monitored. For example, an agent monitoring a business-critical desktop computer collects less data compared to an agent monitoring a server running SQL Server with multiple databases.
- Rate of instance space changes.
  - Updating existing data in the Operations Manager database is resource-intensive compared to writing new operational data. Additionally, when there are changes in instance space data, the management servers need to make more queries to the database to compute configuration and group changes. The rate of instance space changes increases when importing new management packs or adding new agents to the management group.
- The number of Operations Consoles and other SDK connections running simultaneously also affects the load on the database.
  - Each Operations console reads data from the Operations Manager database. Querying this data consumes potentially large amounts of storage I/O resources, CPU time, and RAM. Operations consoles that display large amounts of operational data in the Events View, State View, Alerts View, and Performance Data View tend to cause the largest load on the database.

The Operations Manager database is a single source of failure for the management group, so it can be made highly available using supported failover configurations such as SQL Server Always On Availability Groups or Failover Cluster Instances.

::: moniker range=">=sc-om-2022"

You can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

::: moniker-end

### Enable SQL Broker on Operations Manager database

System Center Operations Manager depends on SQL Server Service Broker to implement all task operations. If SQL Server Service Broker is disabled, all task operations are affected. The resulting behavior can vary according to the task that is initiated. Therefore, it's important to check the state of SQL Server Service Broker whenever unexpected behavior is observed around a task in System Center Operations Manager.

To enable SQL Server Service Broker, follow these steps:

1. Run the following SQL query to check if the broker is already enabled, indicated by a result of **1** (one) in the `is_broker_enabled` field:

   ```SQL
   SELECT is_broker_enabled FROM sys.databases WHERE name='OperationsManager'
   ```

2. If the value that is displayed in the `is_broker_enabled` field is **0** (zero), run the following SQL statement to enable the broker:

   ```SQL
   ALTER DATABASE OperationsManager SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   ALTER DATABASE OperationsManager SET ENABLE_BROKER
   ALTER DATABASE OperationsManager SET MULTI_USER
   ```

### Operations Manager Data Warehouse database

> [!NOTE]
> The Operations Manager Data Warehouse is also referred to as the "Reporting Data Warehouse" database, or just "Data Warehouse" in some documentation.

System Center - Operations Manager inserts data into the data warehouse in near-real time, it's important to have sufficient capacity on this server that supports writing all of the data that is being collected to the data warehouse. As with the Operations Manager database, the most critical resource on the data warehouse is the storage I/O subsystem. On most systems, loads on the data warehouse are similar to the Operations Manager database, but they can vary. In addition, the workload put on the data warehouse by reporting is different than the load put on the Operations Manager database by Operations console usage.

Factors that influence the load on the data warehouse include:

- Rate of operational data collection.
  - The data warehouse performs computations and stores aggregated data, along with a limited amount of raw data, to enable more efficient reporting. As a result, the cost of collecting operational data to the data warehouse is slightly higher compared to the Operations Manager database. However, this cost is offset by the reduced processing cost of discovery data in the data warehouse compared to the Operations Manager database.
- Number of concurrent reporting users or scheduled report generation.
  - Each reporting user can add a significant load on the system because reports frequently summarize large volumes of data. The overall capacity needs are influenced by the number of reports run simultaneously and the type of reports being run. Reports that query large date ranges or large numbers of objects require extra system resources.

Based on these factors, there are several recommended practices to consider when sizing the data warehouse:

- Choose an appropriate storage subsystem.
  - Because the data warehouse is an integral part of the overall data flow through the management group, choosing an appropriate storage subsystem for the data warehouse is important. As with the Operations Manager database, RAID 0 + 1 is often the best choice. In general, the storage subsystem for the data warehouse should be similar to the storage subsystem for the Operations Manager database, and the guidance that applies to the Operations Manager database also applies to the data warehouse.
- Consider appropriate placement of data logs vs. transaction logs.
  - As for the Operations Manager database, separating SQL data and transaction logs are often an appropriate choice as you scale up the number of agents. If both the Operations Manager database and data warehouse are located on the same server and you want to separate data and transaction logs, you must put the transaction logs for the Operations Manager database on a separate physical volume and disk spindles from the data warehouse to receive any benefit. The data files for the Operations Manager database and data warehouse can share the same physical volume as long as the volume provides adequate capacity and disk I/O performance doesn't negatively affect the monitoring and reporting functionality.
- Consider placing the data warehouse on a separate server from the Operations Manager database.
  - Although smaller-scale deployments can often consolidate the Operations Manager database and data warehouse on the same server, it's advantageous to separate them as you scale up the number of agents and the volume of incoming operational data. When the data warehouse and Reporting Server are on a separate server from the Operations Manager database, you experience better reporting performance.

The Operations Manager Data Warehouse database is a single source of failure for the management group, so it can be made highly available using supported failover configurations such as SQL Server Always On Availability Groups or Failover Cluster Instances.

## SQL Server Always On

SQL Server Always On availability groups support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted on an availability replica.

With System Center 2016 and later - Operations Manager, SQL Always On is preferred over failover clustering to provide high availability for databases. All databases except the native mode Reporting Services installation, which uses two databases to separate persistent data storage from temporary storage requirements, can be hosted in an AlwaysOn Availability Group.

To set up an availability group, you deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the Operations Manager SQL Server database as an availability database.

- Learn more about [Always On prerequisites](/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability).
- Learn more about [setting up a WSFC for Always On availability groups](/sql/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server).
- Learn more about [setting up an availability group](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server).

> [!TIP]
> Beginning with Operations Manager 2022, you can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

::: moniker range=">=sc-om-2019"

To set up an availability group, you deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the Operations Manager SQL Server database as an availability database.

- Learn more about [Always On prerequisites](/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability).
- Learn more about [setting up a WSFC for Always On availability groups](/sql/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server).
- Learn more about [setting up an availability group](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server).

> [!NOTE]
> After deploying Operations Manager on the SQL server nodes participating in SQL Always On, to enable [CLR strict security](/sql/database-engine/configure-windows/clr-strict-security?preserve-view=true&view=sql-server-2017), run the [SQL script](upgrade-sqlserver-2019-operations-manager.md#optional---enable-clr-strict-security) on each Operations Manager database.

::: moniker-end

### Multisubnet string

Operations Manager doesn't support the connection string key words (`MultiSubnetFailover=True`). Because an availability group has a listener name (known as the network name or Client Access Point in the WSFC Cluster Manager) depending on multiple IP addresses from different subnets, such as when you deploy in a cross-site failover configuration, client-connection requests from management servers to the availability group listener will hit a connection timeout.

The recommended approach to work around this limitation with deployed availability group server nodes in a multi-subnet environment is to:

1. Set the network name of your availability group listener to only register a single active IP address in DNS.
2. Configure the cluster to use a low TTL value for the registered DNS record.

These settings allow for quicker recovery and resolution of the cluster name with the new IP address when failing over to a node in a different subnet.

Run the following PowerShell commands on any one of the SQL nodes to modify these settings:

```PowerShell
Import-Module FailoverClusters
Get-ClusterResource "Cluster Name"|Set-ClusterParameter RegisterAllProvidersIP 0
Get-ClusterResource "Cluster Name"|Set-ClusterParameter HostRecordTTL 300
Stop-ClusterResource "Cluster Name"
Start-ClusterResource "Cluster Name"
Start-ClusterGroup "Cluster Name"
```

If you're using Always On with a listener name, you should also make these configuration changes on the listener. For more information about configuring an availability group listener, see the documentation here: [Configure availability group listener - SQL Server Always On.](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)

The following PowerShell commands can be run on the SQL node currently hosting the listener to modify its settings:

```PowerShell
Import-Module FailoverClusters
Get-ClusterResource <Listener Cluster Resource name> | Set-ClusterParameter RegisterAllProvidersIP 0
Get-ClusterResource <Listener Cluster Resource name> | Set-ClusterParameter HostRecordTTL 300
Stop-ClusterResource <Listener Cluster Resource name>
Start-ClusterResource <Listener Cluster Resource name>
Start-ClusterGroup <Listener Cluster Group name>
```

When a clustered or an Always On SQL instance is used for high availability, you should enable the automatic recovery feature on your management servers to avoid the Operations Manager Data Access service restart anytime a failover between nodes occur. For configuration information, see the following KB article [The System Center Management service stops responding after an instance of SQL Server goes offline](https://support.microsoft.com/help/2913046/the-system-center-management-service-stops-responding-after-an-instanc).

## Optimize SQL Server

Support experiences have shown that performance issues aren't typically caused by high resource utilization (that is, processor or memory) with SQL Server itself; rather the issue is directly related to the configuration of the storage subsystem. Performance bottlenecks are commonly attributed to not following recommended configuration guidance with the storage provisioned for the SQL Server database instance. Such examples are:

- Insufficient allocation of spindles for the LUNs to support the IO requirements of Operations Manager.
- Hosting transaction logs and database files on the same volume. These two workloads have different IO and latency characteristics.
- Configuration of TempDB is incorrect with respect to placement, sizing, and so on.
- Disk partition misalignment of volumes hosting the database transaction logs, database files, and TempDB.
- Overlooking the basic SQL Server configuration such as using AUTOGROW for database and transaction log files, MAXDOP setting for query parallelism, creating multiple TempDB data files per CPU core, and so on.

Storage configuration is one of the critical components to a SQL Server deployment for Operations Manager. Database servers tend to be heavily I/O bound due to rigorous database read and write activity and transaction log processing. The I/O behavior pattern of Operations Manager is typically 80% writes and 20% reads. As a result, improper configuration of I/O subsystems can lead to poor performance and operation of SQL Server systems and becomes noticeable in Operations Manager.

It's important to test the SQL Server design by performing throughput testing of the IO subsystem before deploying SQL Server. Ensure that these tests are able to achieve your IO requirements with an acceptable latency. Use the [Diskspd Utility](https://github.com/Microsoft/diskspd) to evaluate the I/O capacity of the storage subsystem supporting SQL Server. The following blog article, authored by a member of the File Server team in the product group, provides detailed guidance and recommendations on how to go about performing stress testing using this tool - [DiskSpd, PowerShell, and storage performance: measuring IOPs, throughput and latency for both local disks and SMB file shares](/archive/blogs/josebda/diskspd-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares?branch=main).

### NTFS allocation unit size

Volume alignment, commonly referred to as sector alignment, should be performed on the file system (NTFS) whenever a volume is created on a RAID device. Failure to do so can lead to significant performance degradation and is most commonly the result of partition misalignment with stripe unit boundaries. It can also lead to hardware cache misalignment, resulting in inefficient utilization of the array cache.

When formatting the partition used for SQL Server data files, the recommendation is to use a 64-KB allocation unit size (that is, 65,536 bytes) for data, logs, and TempDB. Be aware, however, that using allocation unit sizes greater than 4-KB results in the inability to use NTFS compression on the volume. While SQL Server does support read-only data on compressed volumes, it isn't recommended.

### Reserve memory

> [!NOTE]
> Much of the information in this section comes from Jonathan Kehayias in his blog post [How much memory does my SQL Server actually need? (sqlskills.com)](https://www.sqlskills.com/blogs/jonathan/how-much-memory-does-my-sql-server-actually-need/).

It's not always easy to identify the right amount of physical memory and processors to allocate for SQL Server in support of System Center Operations Manager (or for other workloads outside of this product). The sizing calculator provided by the product group provides guidance based on workload scale, but its recommendations are based on testing performed in a lab environment that may or may not align with your actual workload and configuration.

SQL Server allows you to [configure the minimum and maximum amount of memory](/sql/database-engine/configure-windows/server-memory-server-configuration-options) that will be reserved and used by its process. By default, SQL Server can change its memory requirements dynamically based on available system resources. The default setting for **min server memory** is 0, and the default setting for **max server memory** is 2,147,483,647 MB.

Performance and memory-related problems can arise if you don't set an appropriate value for **max server memory**. Many factors influence how much memory you need to allocate to SQL Server in order to ensure that the operating system can support other processes running on that system, such as the HBA card, management agents, and anti-virus real-time scanning. If sufficient memory isn't set, the OS and SQL will page to disk. This can cause disk I/O to increase, further decreasing performance and creating a ripple effect where it becomes noticeable in Operations Manager.

We recommend specifying at least 4 GB of RAM for **min server memory**. This should be done for every SQL node hosting one of the Operations Manager databases (operational, data warehouse, ACS).

For **max server memory**, we recommend that you initially reserve a total of:

- 1 GB of RAM for the OS
- 1 GB of RAM per every 4 GB of RAM installed (up to 16-GB RAM)
- 1 GB of RAM per every 8-GB RAM installed (above 16-GB RAM)

After you've set these values, monitor the **Memory\Available MBytes** counter in Windows to determine if you can increase the memory available to SQL Server. Windows signals that the available physical memory is running low at 96 MB, so ideally the counter shouldn't run lower than around 200-300 MB, to ensure you have a buffer. For servers with 256-GB RAM or higher, ensure it doesn't run lower than 1 GB.

Keep in mind that these calculations assume you want SQL Server to be able to use all available memory, unless you modify them to account for other applications. Consider the specific memory requirements for your OS, other applications, the SQL Server thread stack, and other multipage allocators. A typical formula would be `((total system memory) – (memory for thread stack) – (OS memory requirements) – (memory for other applications) – (memory for multipage allocators))`, where the memory for thread stack = `((max worker threads) (stack size))`. The stack size is 512 KB for x86 systems, 2 MB for x64 systems, and 4 MB for IA64 systems, and you can find the value for max worker threads in the max_worker_count column of sys.dm_os_sys_info.

These considerations also apply to the memory requirements for SQL Server to run in a virtual machine. Since SQL Server is designed to cache data in the buffer pool, and it uses as much memory as possible, it can be difficult to determine the ideal amount of RAM needed. When reducing the memory allocated to a SQL Server instance, you can reach a point where lower memory allotment gets traded for higher disk I/O access.

To configure SQL Server memory in an environment that has been over-provisioned, start by monitoring the environment and the current performance metrics, including the SQL Server Buffer Manager **page life expectancy** and **page reads/sec** and the Physical Disk **disk reads/sec** values. If the environment has excess memory, **page life expectancy** will increase by a value of one each second without any decrease under the workload, due to caching; the SQL Server Buffer Manager **page reads/sec** value will be low after the cache ramps up; and the Physical Disk **disk reads/sec** will also remain low.

Once you understand the environment baseline, you can reduce the **max server memory** by 1 GB, then see how that impacts your performance counters (after any initial cache flushing subsides). If the metrics remain acceptable, reduce by another 1 GB, then monitor again, repeating as desired until you determine an ideal configuration.

::: moniker range="=sc-om-2016"

For more information, see [Server memory configuration options](/sql/database-engine/configure-windows/server-memory-server-configuration-options?preserve-view=true&view=sql-server-2014).

::: moniker-end

For more information, see [Server memory configuration options](/sql/database-engine/configure-windows/server-memory-server-configuration-options?preserve-view=true&view=sql-server-2016).

### Optimize TempDB

The size and physical placement of the TempDB database can affect the performance of Operations Manager. For example, if the size that is defined for TempDB is too small, part of the system-processing load may be taken up with autogrowing TempDB to the size required to support the workload every time you restart the instance of SQL Server.
To achieve optimal TempDB performance, we recommend the following configuration for TempDB in a production environment:

- Set the [recovery model](/sql/relational-databases/backup-restore/recovery-models-sql-server) of TempDB to SIMPLE.
  - This model automatically reclaims log space to keep space requirements small.
- Preallocate space for all TempDB files by setting the file size to a value large enough to accommodate the typical workload in the environment. It prevents TempDB from expanding too frequently, which can affect performance. The TempDB database can be set to autogrow, but this should be used to increase disk space for unplanned exceptions.
- Create as many files as needed to maximize disk bandwidth.
  - Using multiple files reduces TempDB storage contention and yields improved scalability. However, don't create too many files as it can reduce performance and increase management overhead.
  - As a general guideline, create one data file for each logical processor on the server (accounting for any affinity mask settings) and then adjust the number of files up or down as necessary.
  - As a general rule, if the number of logical processors is less than or equal to 8, use the same number of data files as logical processors. 
    - If the number of logical processors is greater than 8, use eight data files and then if contention continues, increase the number of data files by multiples of 4 (up to the number of logical processors) until the contention is reduced to acceptable levels or make changes to the workload/code.
    - If the contention isn't reduced, you may have to increase the number of data files more.
- Make each data file the same size, allowing for optimal proportional-fill performance.
  - The equal sizing of data files is critical because the proportional fill algorithm is based on the size of the files. If data files are created with unequal sizes, the proportional fill algorithm tries to use the largest file more for GAM allocations instead of spreading the allocations between all the files, thereby defeating the purpose of creating multiple data files.
- Put the TempDB database on a fast I/O subsystem using solid-state drives for the most optimal performance.
  - Use disk striping if there are many directly attached disks.
- Put the TempDB database on disks that differ from those that are used by user databases.

To configure TempDB, you can run the following query or modify its properties in Management Studio.

```SQL
USE [TempDB]
GO
DBCC SHRINKFILE (N'tempdev' , 8)
GO
USE [master]
GO
ALTER DATABASE [TempDB] MODIFY FILE ( NAME = N'tempdev', NEWNAME = N'TempDB', SIZE = 2097152KB , FILEGROWTH = 512MB )
GO
ALTER DATABASE [TempDB] ADD FILE ( NAME = N'TempDB2', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\DATA\TempDB2.mdf' , SIZE = 2097152KB , FILEGROWTH = 512MB )
GO
```

Run the T-SQL query `SELECT * from sys.sysprocesses` to detect page allocation contention for the TempDB database. In the system table output, the wait resource can appear as "2:1:1" (PFS Page) or "2:1:3" (Shared Global Allocation Map Page). Depending on the degree of contention, this setting could lead to SQL Server appearing unresponsive for short periods. Another approach is to examine the Dynamic Management Views [sys.dm_exec_request or sys.dm_os_waiting_tasks]. The results show that these requests or tasks are waiting for TempDB resources and have similar values as highlighted earlier when you execute the `sys.sysprocesses` query.

If the previous recommendations don't significantly reduce the allocation contention and the contention is on SGAM pages, [implement trace flag](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql) `-T1118` in the Startup parameters for SQL Server so that the trace flag remains in effect even after SQL Server is recycled. Under this trace flag, SQL Server allocates full extents to each database object, thereby eliminating the contention on SGAM pages.

> [!NOTE]
> This trace flag affects every database on the instance of SQL Server.

### Max degree of parallelism

> [!TIP]
> For the latest best practices and recommendations from the SQL Server team, refer to their documentation here: [Set the max degree of parallelism option for optimal performance](/sql/relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance)

The default configuration of SQL Server for small to medium size deployments of Operations Manager is adequate for most needs. However, when the workload of the management group scales upwards towards an enterprise class scenario (typically 2,000+ agent-managed systems and an advanced monitoring configuration, which includes service-level monitoring with advanced synthetic transactions, network device monitoring, cross-platform, and so forth) it's necessary to optimize the configuration of SQL Server described in this section of the document. One configuration option not discussed in previous guidance is MAXDOP.

The Microsoft SQL Server max degree of parallelism (MAXDOP) configuration option controls the number of processors that are used for the execution of a query in a parallel plan. This option determines the computing and thread resources that are used for the query plan operators that perform the work in parallel. Depending on whether SQL Server is set up on a symmetric multiprocessing (SMP) computer, a nonuniform memory access (NUMA) computer, or hyperthreading-enabled processors, you've to configure the max degree of parallelism option appropriately.

When SQL Server runs on a computer with more than one microprocessor or CPU, it detects the best degree of parallelism, that is, the number of processors employed to run a single statement, for each parallel plan execution. By default, its value for this option is 0, which allows SQL Server to determine the maximum degree of parallelism.

The stored procedures and queries predefined in Operations Manager as it relates to the operational, data warehouse, and even audit database don't include the MAXDOP option, as there's no way during installation to dynamically query how many processors are presented to the operating system, nor does it attempt to hardcode the value for this setting, which could have negative consequences when the query is executed.

> [!NOTE]
> The max degree of parallelism configuration option doesn't limit the number of processors that the SQL Server uses. To configure the number of processors that SQL Server uses, use the affinity mask configuration option.

- For servers that use more than eight processors, use the following configuration:
MAXDOP=8
- For servers that use eight or fewer processors, use the following configuration:
MAXDOP=0 to N
  
  > [!TIP]
  > In this configuration, `N` represents the number of processors.

- For servers that have NUMA configured, MAXDOP shouldn't exceed the number of CPUs that are assigned to each NUMA node.
- For servers that have hyperthreading enabled, the MAXDOP value shouldn't exceed the number of physical processors.
- For servers that have NUMA configured and hyperthreading enabled, the MAXDOP value shouldn't exceed the number of physical processors per NUMA node.

You can monitor the number of parallel workers by querying `select * from sys.dm_os_tasks`.

In this example, the hardware configuration of the server was an HP Blade G6 with 24 core processors and 196 GB of RAM. The instance hosting the Operations Manager database had a MAXMEM setting of 64 GB. After performing the suggested optimizations in this section, performance improved. However, a query parallelism bottleneck still persisted. After testing different values, the most optimal performance was found by setting MAXDOP=4.

### Initial database sizing

Attempting to estimate the future growth of the Operations Manager databases, specifically the operational and data warehouse databases, within the first several months after deployment isn't a simple exercise. While the [Operations Manager Sizing Helper](https://techcommunity.microsoft.com/t5/system-center-blog/operations-manager-2012-sizing-helper-tool/ba-p/345075) is reasonable in estimating potential growth based on the formula derived by the product group from their testing in the lab, it doesn't take into account several factors, which can influence growth in the near term versus long term.

The initial database size, as suggested by the Sizing Helper, should be allocated to a predicted size to reduce fragmentation and corresponding overhead, which can be specified at setup time for the Operational and Data Warehouse databases. If during setup not enough storage space is available, the databases can be expanded later by using SQL Management Studio and then reindexed thereafter to defragment and optimize accordingly. This recommendation applies to the ACS database also.

Proactive monitoring of the growth of the operational and data warehouse database should be performed on a daily or weekly cycle. This is necessary to identify unexpected and significant growth spurts, and begin troubleshooting in order to determine causality, whether by a bug in a management pack workflow (that is, discovery rule, performance or event collection rule, or monitor or alert rule) or other symptom with a management pack that wasn't identified during testing and quality assurance phase of the release management process.

### Database autogrow

When the reserved databases file size becomes full, SQL Server can automatically increase the size by a percentage or by a fixed amount. Moreover, a maximum database size can be configured to prevent filling up all the space available on disk. By default, the Operations Manager database isn't configured with autogrow enabled; only the Data Warehouse and ACS databases are.

Only rely on autogrow as a contingency for unexpected growth. Autogrow introduces a performance penalty that should be considered when dealing with a highly transactional database. Performance penalties include:

- If you don’t provide an appropriate growth increment, fragmentation of the log file or database can occur.
- If you run a transaction that requires more log space than is available, and autogrow is enabled for the transaction log of that database, the time it takes the transaction to complete will include the time it takes the transaction log to grow by the configured amount.
- If you run a large transaction that requires the log to grow, other transactions that require a write to the transaction log will also have to wait until the grow operation completes.

If the autogrow and autoshrink options are combined, this can create unnecessary overhead. Ensure that the thresholds that trigger the grow and shrink operations won't cause frequent up and down size changes. For example, you may run a transaction that causes the transaction log to grow by 100 MB by the time it commits; some time after that autoshrink starts and shrinks the transaction log by 100 MB. Then you run the same transaction, and it causes the transaction log to grow by 100 MB again. In that example, you're creating unnecessary overhead and potentially creating fragmentation of the log file, either of which can negatively affect performance.

Configure these two settings carefully. The particular configuration really depends on your environment. The general recommendation is to increase database size by a fixed amount in order to reduce disk fragmentation. See, for example, the following figure, where the database is configured to grow by 1,024 MB each time autogrow is required.

### Cluster failover policy

Windows Server Failover Clustering is a high availability platform that is constantly monitoring the network connections and health of the nodes in a cluster. If a node isn't reachable over the network, then recovery action is taken to recover and bring applications and services online on another node in the cluster. The default settings out of the box are optimized for failures where there's a complete loss of a server, which is considered a "hard" failure. These would be unrecoverable failure scenarios such as the failure of nonredundant hardware or power. In these situations, the server is lost and the goal is for Failover Clustering to quickly detect the loss of the server and rapidly recover on another server in the cluster. To accomplish this fast recovery from hard failures, the default settings for cluster health monitoring are fairly aggressive. However, they're fully configurable to allow flexibility for various scenarios.

These default settings deliver the best behavior for most customers; however, as clusters are stretched from being inches to possibly miles apart, the cluster may become exposed to more, and potentially unreliable, networking components between the nodes. Another factor is that the quality of commodity servers is constantly increasing, coupled with augmented resiliency through redundant components (such as dual power supplies, NIC teaming, and multi-path I/O), the number of nonredundant hardware failures may potentially be fairly rare. Because hard failures may be less frequent, some customers may wish to tune the cluster for transient failures, where the cluster is more resilient to brief network failures between the nodes. By increasing the default failure thresholds, you can decrease the sensitivity to brief network issues that last a short period of time.

It's important to understand that there's no right answer here, and the optimized setting may vary by your specific business requirements and service level agreements.

### Virtualizing SQL Server

In virtual environments, for performance reasons, it's recommended that you store the operational database and data warehouse database on a direct attached storage, and not on a virtual disk. You can use the [Operations Manager Sizing Helper](https://techcommunity.microsoft.com/t5/system-center-blog/operations-manager-2012-sizing-helper-tool/ba-p/345075) utility released for Operations Manager 2012 to estimate required IOPS and stress test your data disks to verify. Storage performance can be tested with the [DiskSpd utility](https://github.com/microsoft/diskspd). See also [Operations Manager virtualization support](./system-requirements.md#virtualization) for additional guidance on virtualized Operations Manager environment.

### Always On and recovery model

Although not strictly an optimization, an important consideration regarding Always On Availability Group is the fact that, by design, this feature requires the databases to be set in the “Full” recovery model. Meaning, the transaction logs are never discarded until either a full backup is done or only the transaction log.
For this reason, a backup strategy isn't an optional but a required part of the AlwaysOn design for Operations Manager databases. Otherwise, with time, disks containing transaction logs fill up.

A backup strategy must take into account the details of your environment. A typical backup schedule is given in the following table.

|Backup Type | Schedule |
|-----------|---------------|
| Transaction log only | Every one hour |
| Full | Weekly, Sunday at 3:00 AM |

## Optimizing SQL Server reporting services

The Reporting Services instance acts as a proxy for access to data in the Data Warehouse database. It generates and displays reports based on templates stored inside the management packs.

The Operations Manager Reporting role can't be installed in a side-by-side fashion with a previous version of the Reporting role and **must** be installed in native mode only (SharePoint integrated mode isn't supported).

Behind the scenes of Reporting Services, there's a SQL Server Database instance that hosts the ReportServer and ReportServerTempDB databases. General recommendations regarding the performance tuning of this instance apply.

> [!NOTE]
> From SQL Server Reporting Services (SSRS) 2017 version 14.0.600.1274 and later, the default security settings don't allow resource extension uploads. This leads to **ResourceFileFormatNotAllowedException** exceptions in Operations Manager during deployment of reporting components.
>
> To fix this:
>
> 1. Open SQL Management Studio.
> 1. Connect to your Reporting Services instance.
> 1. Right-click on the server instance in the Object Explorer window.
> 1. Select **Properties**.
> 1. Select **Advanced** on the left sidebar.
> 1. Add `*.*` to the list for *AllowedResourceExtensionsForUpload*.
>
> Alternatively, you can add the full list of Operations Manager's reporting extensions to the *allow list* in SSRS. The list is described in "Resolution 2" here: [Operations Manager reports fail to deploy](/troubleshoot/system-center/scom/cannot-deploy-operations-manager-reports)

## Next steps

To understand how to configure hosting the (Reporting) Data Warehouse behind a firewall, see [Connect the (Reporting) Data Warehouse Across a Firewall](deploy-connect-reportingdw-firewall.md).
