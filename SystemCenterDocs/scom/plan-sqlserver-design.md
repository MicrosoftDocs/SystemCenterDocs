---
ms.assetid: 5a3a8b98-1113-45bf-9484-2c807ec3d013
title: SQL Server Design Considerations
description: This article provides detailed design guidance for SQL Server to support the Operations Manager databases and reporting component.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 03/07/2024
ms.custom: engagement-fy23, UpdateFrequency.5
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# SQL Server Design Considerations

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

System Center Operations Manager requires access to an instance of a server running Microsoft SQL Server to support the operational, data warehouse, and ACS audit database. The operational and data warehouse databases are required and created when you deploy the first management server in your management group, while the ACS database is created when you deploy an ACS collector in your management group.  

In a lab environment or small-scale deployment of Operations Manager, SQL Server can be co-located on the first management server in the management group.

In a medium to enterprise-scale distributed deployment, the SQL Server instance should be located on a dedicated standalone server or in a SQL Server high-availability configuration. In either case, SQL Server must already exist and is accessible before you start the installation of the first management server or ACS collector.

We don't recommend utilization of Operations Manager databases from an SQL Instance that has other application databases. This is to avoid any potential issues with I/O and other hardware resource restrictions.

> [!IMPORTANT]
> Operations Manager does not support Platform as a Service (PaaS) instances of SQL, including products such as Azure SQL Managed Instance or Amazon Relational Database Service (AWS RDS). Please use an instance of SQL Server installed on a Windows machine. The only exception to this is within [Azure Monitor SCOM Managed Instance](./operations-manager-managed-instance-overview.md), which utilizes Azure SQL MI, and is not reconfigurable.

## SQL Server requirements

::: moniker range=">sc-om-1807"

The following versions of SQL Server Enterprise & Standard Edition are supported for an existing installation of System Center Operations Manager version to host Reporting Server, Operational, Data Warehouse, and ACS database:

::: moniker-end

::: moniker range="sc-om-2019"

- SQL Server 2019 with Cumulative Update 8 (CU8) or later as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)

  >[!NOTE]
  > - Operations Manager 2019 supports SQL 2019 with CU8 or later; however, it doesn't support SQL 2019 RTM.
  > - Use ODBC 17.3 or 17.10.5 or later, and MSOLEDBSQL 18.2 or 18.6.7 or later.

::: moniker-end

::: moniker range=">=sc-om-2022"

- SQL Server 2022
- SQL Server 2019 with Cumulative Update 8 (CU8) or later as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)

  >[!NOTE]
  > - Operations Manager 2022 and later supports SQL 2019 with CU8 or later; however, it doesn't support SQL 2019 RTM.
  > - Use ODBC 17.3 or later, and MSOLEDBSQL 18.2 or later.

::: moniker-end

::: moniker range=">sc-om-1807 <=sc-om-2019"

- SQL Server 2017 and Cumulative Updates as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)
- SQL Server 2016 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)

::: moniker-end

::: moniker range=">=sc-om-2022"

- SQL Server 2017 and Cumulative Updates as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)

::: moniker-end

::: moniker range="sc-om-1807"

The following versions of SQL Server Enterprise & Standard Edition are supported for an existing installation of System Center Operations Manager version to host Reporting Server, Operational, Data Warehouse, and ACS database:

* SQL Server 2017 and Cumulative Updates as detailed [here](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)
* SQL Server 2016 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)

::: moniker-end

::: moniker range=">=sc-om-2019"

Before upgrading SQL Server, see [upgrade information for 2017](upgrade-sqlserver-2017-opsmgr.md) and [upgrade information for SQL 2019](upgrade-sqlserver-2019-operations-manager.md).

::: moniker-end

::: moniker range="sc-om-1807"

Before upgrading to SQL Server 2017, see [upgrade information for 2017](upgrade-sqlserver-2017-opsmgr.md).

::: moniker-end

::: moniker range="sc-om-1801"

The following versions of SQL Server Enterprise & Standard Edition are supported for a new or existing installation of System Center Operations Manager version 1801 to host Reporting Server, Operational, Data Warehouse, and ACS database:

* SQL Server 2016 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)

::: moniker-end

::: moniker range="sc-om-2016"
The following versions of SQL Server Enterprise & Standard Edition are supported for a new or existing installation of System Center 2016 - Operations Manager to host Reporting Server, Operational, Data Warehouse, and ACS database:

* SQL Server 2016 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2016)
* SQL Server 2014 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2014)
* SQL Server 2012 and Service Packs as detailed [here](/lifecycle/products/?terms=SQL+Server+2012)

::: moniker-end

> [!NOTE]
> - Each of the following SQL Server components supporting a SCOM infrastructure are required to be at the same SQL Server major version: 
>    - SQL Server database engine instances hosting any of the SCOM databases (that is, **OperationManager**, **OperationManagerDW**, and SSRS databases **ReportServer** & **ReportServerTempDB**).
>    - SQL Server Reporting Services (SSRS) instance.
> - The SQL Server collation setting must be one of the supported types as described in the [**SQL Server collation setting**](#sql-server-collation-setting) section below.
> - SQL Server Full Text Search is required for all SQL Server database engine instances hosting any of the SCOM databases.
> - The Windows Server 2016 installation options (Server Core, Server with Desktop Experience, and Nano Server) supported by Operations Manager database components are based on what installation options of Windows Server are supported by SQL Server.

> [!NOTE]
> System Center Operations Manager Reporting cannot be installed in a side-by-side fashion with a previous version of the Reporting role and **must** be installed in native mode only (SharePoint integrated mode isn't supported).

Additional hardware and software considerations apply in your design planning:

- We recommend that you run SQL Server on computers with the NTFS file format.
- There must be at least 1024 MB of free disk space for the operational and data warehouse database. It's enforced at the time of database creation, and it will likely grow significantly after setup.  
- .NET Framework 4 is required.
- .NET Framework 4.8 is supported from Operations Manager 2022.
- Reporting Server isn't supported on Windows Server Core.

::: moniker range="=sc-om-2016"

For more information, see Hardware and Software Requirements for Installing SQL Server [2014](/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?preserve-view=true&view=sql-server-2014) or [2016](/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?preserve-view=true&view=sql-server-2016).

::: moniker-end

::: moniker range=">=sc-om-1801"

For more information, see [Hardware and Software Requirements for Installing SQL Server](/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?preserve-view=true&view=sql-server-2016).

::: moniker-end

> [!NOTE]
> Although Operations Manager uses only Windows authentication during installation, the SQL Mixed Mode Authentication setting will still work if no local account has the db_owner role. Local accounts with the db_owner role are known to cause issues with System Center Operations Manager. Remove the db_owner role from all the local accounts before installing the product and don’t add the db_owner role to any of the local accounts after installation.

## SQL Server collation setting

The following SQL Server and Windows collations are supported by System Center Operations Manager.

>[!NOTE]
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

If your SQL Server instance isn't configured with one of the supported collations listed earlier, performing a new setup of Operations Manager setup will fail.  However, an in-place upgrade will complete successfully.  

## Firewall configuration

Operations Manager depends on SQL Server to host its databases and a reporting platform to analyze and present historical operational data. The management server, Operations, and Web console roles need to be able to successfully communicate with SQL Server, and it's important to understand the communication path and ports in order to configure your environment correctly.  

If you're designing a distributed deployment that will require SQL Always On Availability Groups to provide failover functionality for the Operations Manager databases, there are additional firewall configuration settings that need to be included in your firewall security strategy.

The following table helps you identify the firewall ports required by SQL Server that will need to be allowed at a minimum in order for server roles in your Operations Manager management group to successfully communicate.

| Scenario | Port | Direction | Operations Manager Role |
|-----------|---------------|---------------|---------------|
| SQL Server hosting Operations Manager databases | TCP 1433 \* | Inbound | management server and Web console (for Application Advisor and Application Diagnostics) |
| SQL Server Browser service | UDP 1434 | Inbound | management server |
| SQL Server Dedicated Admin Connection | TCP 1434 | Inbound | management server |
| Additional ports used by SQL Server<br> - Microsoft remote procedure calls (MS RPC)<br> - Windows Management Instrumentation (WMI)<br> - Microsoft Distributed Transaction Coordinator (MS DTC)| TCP 135 | Inbound | management server |
| SQL Server Always On Availability Group Listener | Administrator configured port | Inbound | management server
| SQL Server Reporting Services hosting Operations Manager Reporting Server | TCP 80 (default)/443 (SSL) | Inbound | management server and Operations console |  

\* While TCP 1433 is the standard port for the default instance of the Database Engine, when you create a named instance on a standalone SQL Server or have deployed a SQL Always On Availability Group, a custom port will be defined and should be documented for reference so that you properly configure your firewalls and enter this information during setup.

For a more detailed overview of the firewall requirements for SQL Server, see [Configure the Windows Firewall to Allow SQL Server Access](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).

## Capacity and storage considerations

### Operations Manager database

The Operations Manager database is a SQL Server database that contains all of the data needed by Operations Manager for day-to-day monitoring.  Sizing and configuration of the database server is critical to the overall performance of the management group.  The most critical resource used by the Operations Manager database is the storage subsystem, but CPU and RAM are also significant.

Factors that influence the load on the Operations Manager database include:

- Rate of operational data collection.  Operational data consists of all the events, alerts, state changes, and performance data collected by agents.  Most of the resources that are used by the Operations Manager database are used to write this data to disk as it comes into the system.  The rate of operational data collected tends to increase as additional management packs are imported and additional agents are added.  The type of computer that an agent is monitoring is also an important factor used when determining the overall rate of operational data collection.  For example, an agent that is monitoring a business-critical desktop computer can be expected to collect less data than an agent monitoring a server that is running an instance of SQL Server with a large number of databases.
- Rate of instance space changes.  Updating this data in the Operations Manager database is costly relative to writing new operational data.  In addition, when instance space data changes, the management servers make additional queries to the Operations Manager database in order to compute configuration and group changes.  The rate of instance space changes increases as you import additional management packs into a management group.  Adding new agents to a management group also temporarily increases the rate of instance space changes.
- Number of Operations Consoles and other SDK connections running simultaneously.  Each Operations console reads data from the Operations Manager database.  Querying this data consumes potentially large amounts of storage I/O resources, CPU time, and RAM. Operations consoles that display large amounts of operational data in the Events View, State View, Alerts View, and Performance Data View tend to cause the largest load on the database.  

The Operations Manager database is a single source of failure for the management group, so it can be made highly available using supported failover configurations such as SQL Server Always On Availability Groups or Failover Cluster Instances.

::: moniker range=">=sc-om-2022"

You can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

::: moniker-end

### Enable SQL Broker on Operations Manager database

System Center Operations Manager depends on SQL Server Service Broker to implement all task operations. If SQL Server Service Broker is disabled, all task operations will be affected. The resulting behavior may vary according to the task that is initiated. Therefore, it's important to check the state of SQL Server Service Broker whenever unexpected behavior is observed around a task in System Center Operations Manager.

To enable SQL Server Service Broker, follow these steps:

1. Run the following SQL query:

   ```SQL
   SELECT is_broker_enabled FROM sys.databases WHERE name='OperationsManager'
   ```

2. Skip this step if the value that is displayed in the `is_broker_enabled` field is **1** (one). Otherwise, run the following SQL queries:

   ```SQL
   ALTER DATABASE OperationsManager SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   ALTER DATABASE OperationsManager SET ENABLE_BROKER
   ALTER DATABASE OperationsManager SET MULTI_USER
   ```

### Operations Manager data warehouse database

System Center - Operations Manager inserts data into the Reporting data warehouse in near-real time, it's important to have sufficient capacity on this server that supports writing all of the data that is being collected to the Reporting data warehouse.  As with the Operations Manager database, the most critical resource on the Reporting data warehouse is the storage I/O subsystem.  On most systems, loads on the Reporting data warehouse are similar to the Operations Manager database, but they can vary.  In addition, the workload put on the Reporting data warehouse by reporting is different than the load put on the Operations Manager database by Operations console usage.

Factors that influence the load on the Reporting data warehouse include:

- Rate of operational data collection.  To allow for more efficient reporting, the Reporting data warehouse computes and stores aggregated data in addition to a limited amount of raw data.  Doing this extra work means that operational data collection to the Reporting data warehouse can be slightly more costly than to the Operations Manager database.  This additional cost is typically balanced by the reduced cost of processing discovery data by the Reporting data warehouse versus the Operations Manager database.
- Number of concurrent reporting users or scheduled report generation.  Because reports frequently summarize large volumes of data, each reporting user can add a significant load on the system.  The number of reports run simultaneously and the type of reports being run both affect overall capacity needs.  Generally, reports that query large date ranges or large numbers of objects require additional system resources.

Based on these factors, there are several recommended practices to consider when sizing the Reporting data warehouse:

- Choose an appropriate storage subsystem.  Because the Reporting data warehouse is an integral part of the overall data flow through the management group, choosing an appropriate storage subsystem for the Reporting data warehouse is important.  As with the Operations Manager database, RAID 0 + 1 is often the best choice.  In general, the storage subsystem for the Reporting data warehouse should be similar to the storage subsystem for the Operations Manager database, and the guidance that applies to the Operations Manager database also applies to the Reporting data warehouse.
- Consider appropriate placement of data logs vs. transaction logs.  As for the Operations Manager database, separating SQL data and transaction logs are often an appropriate choice as you scale up the number of agents.  If both the Operations Manager database and Reporting data warehouse are located on the same server and you want to separate data and transaction logs, you must put the transaction logs for the Operations Manager database on a separate physical volume and disk spindles from the Reporting data warehouse to receive any benefit.  The data files for the Operations Manager database and Reporting data warehouse can share the same physical volume as long as the volume provides adequate capacity and disk I/O performance doesn't negatively affect the monitoring and reporting functionality.
- Consider placing the Reporting data warehouse on a separate server from the Operations Manager database.  Although smaller-scale deployments can often consolidate the Operations Manager database and Reporting data warehouse on the same server, it's advantageous to separate them as you scale up the number of agents and the volume of incoming operational data.  When the Reporting data warehouse and Reporting Server are on a separate server from the Operations Manager database, you experience better reporting performance.

The Operations Manager data warehouse database is a single source of failure for the management group, so it can be made highly available using supported failover configurations such as SQL Server Always On Availability Groups or Failover Cluster Instances.  

::: moniker range="<=sc-om-1807"

## SQL Server Always On

SQL Server Always On availability groups support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted by an availability replica.

With System Center 2016 and later - Operations Manager, SQL Always On is preferred over failover clustering to provide high availability for databases. All databases except the native mode Reporting Services installation, which uses two databases to separate persistent data storage from temporary storage requirements, can be hosted in an AlwaysOn Availability Group.

To set up an availability group you'll need to deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the Operations Manager SQL Server database as an availability database.

- Learn more about [Always On prerequisites](/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability).
- Learn more about [setting up a WSFC for Always On availability groups](/sql/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server).
- Learn more about [setting up an availability group](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server).

::: moniker-end

::: moniker range=">=sc-om-2019"

## SQL Server Always On

SQL Server Always On availability groups support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted by an availability replica.

With System Center 2016 and later - Operations Manager, SQL Always On is preferred over failover clustering to provide high availability for databases. All databases except the native mode Reporting Services installation, which uses two databases to separate persistent data storage from temporary storage requirements, can be hosted in an AlwaysOn Availability Group.  

::: moniker-end

::: moniker range=">=sc-om-2022"

You can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

::: moniker-end

::: moniker range=">=sc-om-2019"

To set up an availability group, you'll need to deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the Operations Manager SQL Server database as an availability database.

- Learn more about [Always On prerequisites](/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability).
- Learn more about [setting up a WSFC for Always On availability groups](/sql/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server).
- Learn more about [setting up an availability group](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server).

> [!NOTE]
> After deploying Operations Manager on the SQL server nodes participating in SQL Always On, to enable [CLR strict security](/sql/database-engine/configure-windows/clr-strict-security?preserve-view=true&view=sql-server-2017), run the [SQL script](upgrade-sqlserver-2019-operations-manager.md#optional---enable-clr-strict-security) on each Operations Manager database.

::: moniker-end

### Multisubnet string

Operations Manager doesn't support the connection string key words (MultiSubnetFailover=True).  Because an availability group has a listener name (known as the network name or Client Access Point in the WSFC Cluster Manager) depending on multiple IP addresses from different subnets, such as when you deploy in a cross-site failover configuration, client-connection requests from management servers to the availability group listener will hit a connection timeout.  

The recommended approach to work around this limitation when you've deployed server nodes in the availability group in a multi-subnet environment is to do the following:

1. Set the network name of your availability group listener to only register a single active IP address in DNS.
2. Configure the cluster to use a low TTL value for the registered DNS record.

These settings allow, when failover to a node in a different subnet, for quicker recovery and resolution of the cluster name with the new IP address.

Run the following PowerShell commands on any one of the SQL nodes to modify its settings:

  ```PowerShell
  Import-Module FailoverClusters
  Get-ClusterResource "Cluster Name"|Set-ClusterParameter RegisterAllProvidersIP 0
  Get-ClusterResource "Cluster Name"|Set-ClusterParameter HostRecordTTL 300
  Stop-ClusterResource "Cluster Name"
  Start-ClusterResource "Cluster Name"
  Start-ClusterGroup "Cluster Name"
  ```

If you're using Always On with a listener name, you should also make these configuration changes on the listener. For more information about configuring an availability group listener, see the documentation here: [Configure availability group listener - SQL Server Always On](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)

Run the following PowerShell commands on the SQL node currently hosting the listener to modify its settings:

  ```PowerShell
  Import-Module FailoverClusters
  Get-ClusterResource <Listener Cluster Resource name> | Set-ClusterParameter RegisterAllProvidersIP 0
  Get-ClusterResource <Listener Cluster Resource name> | Set-ClusterParameter HostRecordTTL 300
  Stop-ClusterResource <Listener Cluster Resource name>
  Start-ClusterResource <Listener Cluster Resource name>
  Start-ClusterGroup <Listener Cluster Group name>
  ```

When a clustered or an Always On SQL instance is used for high availability, you should enable the automatic recovery feature on your management servers to avoid the Operations Manager Data Access service restart anytime a failover between nodes occur.  For information on how to configure this, see the following KB article [The System Center Management service stops responding after an instance of SQL Server goes offline](https://support.microsoft.com/help/2913046/the-system-center-management-service-stops-responding-after-an-instanc).

## Optimize SQL Server

In general, previous deployment experience with customers shows that performance issues are typically not caused by high resource utilization (that is, processor or memory) with SQL Server itself; rather it's directly related to the configuration of the storage subsystem.  Performance bottlenecks are commonly attributed to not following recommended configuration guidance with the storage provisioned for the SQL Server database instance.  Such examples are:

- Insufficient allocation of spindles for the LUNs to support the IO requirements of Operations Manager.  
- Hosting transaction logs and database files on the same volume.  These two workloads have different IO and latency characteristics.
- Configuration of TempDB is incorrect with respect to placement, sizing, and so on.
- Disk partition misalignment of volumes hosting the database transaction logs, database files, and TempDB.
- Overlooking the basic SQL Server configuration such as using AUTOGROW for database and transaction log files, MAXDOP setting for query parallelism, creating multiple TempDB data files per CPU core, and so on.

Storage configuration is one of the critical components to a SQL Server deployment for Operations Manager.  Database servers tend to be heavily I/O bound due to rigorous database read and write activity and transaction log processing.  The I/O behavior pattern of Operations Manager is typically 80% writes and 20% reads.  As a result, improper configuration of I/O subsystems can lead to poor performance and operation of SQL Server systems and becomes noticeable in Operations Manager.

It's important to test the SQL Server design by performing throughput testing of the IO subsystem prior to deploying SQL Server. Ensure that these tests are able to achieve your IO requirements with an acceptable latency.  Use the [Diskspd Utility](https://github.com/Microsoft/diskspd) to evaluate the I/O capacity of the storage subsystem supporting SQL Server.  The following blog article, authored by a member of the File Server team in the product group, provides detailed guidance and recommendations on how to go about performing stress testing using this tool with some PowerShell code and [capturing the results using PerfMon](/archive/blogs/josebda/sqlio-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares).  You can also refer to the [Operations Manager Sizing Helper](https://techcommunity.microsoft.com/t5/system-center-blog/operations-manager-2012-sizing-helper-tool/ba-p/345075)  for initial guidance.

### NTFS allocation unit size

Volume alignment, commonly referred to as sector alignment, should be performed on the file system (NTFS) whenever a volume is created on a RAID device. Failure to do so can lead to significant performance degradation and is most commonly the result of partition misalignment with stripe unit boundaries. It can also lead to hardware cache misalignment, resulting in inefficient utilization of the array cache.
When formatting the partition that will be used for SQL Server data files, it's recommended that you use a 64-KB allocation unit size (that is, 65,536 bytes) for data, logs, and tempdb. Be aware, however, that using allocation unit sizes greater than 4 KB results in the inability to use NTFS compression on the volume. While SQL Server does support read-only data on compressed volumes, it isn't recommended.

### Reserve memory

> [!NOTE]
> Much of the information in this section comes from Jonathan Kehayias in his blog post [How much memory does my SQL Server actually need? (sqlskills.com)](https://www.sqlskills.com/blogs/jonathan/how-much-memory-does-my-sql-server-actually-need/).

It's not always easy to identify the right amount of physical memory and processors to allocate for SQL Server in support of System Center Operations Manager (or for other workloads outside of this product).  The sizing calculator provided by the product group provides guidance based on workload scale, but its recommendations are based on testing performed in a lab environment that may or may not align with your actual workload and configuration.

SQL Server allows you to [configure the minimum and maximum amount of memory](/sql/database-engine/configure-windows/server-memory-server-configuration-options) that will be reserved and used by its process. By default, SQL Server can change its memory requirements dynamically based on available system resources. The default setting for **min server memory** is 0, and the default setting for **max server memory** is 2,147,483,647 MB.

Performance and memory-related problems can arise if you don't set an appropriate value for **max server memory**. Many factors influence how much memory you need to allocate to SQL Server in order to ensure that the operating system can support other processes running on that system, such as the HBA card, management agents, and anti-virus real-time scanning. If sufficient memory isn't set, the OS and SQL will page to disk. This can cause disk I/O to increase, further decreasing performance and creating a ripple effect where it becomes noticeable in Operations Manager.  

We recommend specifying at least 4 GB of RAM for **min server memory**. This should be done for every SQL node hosting one of the Operations Manager databases (operational, data warehouse, ACS).

For **max server memory**, we recommend that you initially reserve a total of:

- 1 GB of RAM for the OS
- 1 GB of RAM per every 4 GB of RAM installed (up to 16-GB RAM)
- 1 GB of RAM per every 8-GB RAM installed (above 16-GB RAM)

After you've set these values, monitor the **Memory\Available MBytes** counter in Windows to determine if you can increase the memory available to SQL Server. Windows signals that the available physical memory is running low at 96 MB, so ideally the counter shouldn't run lower than around 200-300 MB, to ensure you've a buffer. For servers with 256-GB RAM or higher, you'll probably want to ensure it doesn't run lower than 1 GB.

Keep in mind that these calculations assume you want SQL Server to be able to use all available memory, unless you modify them to account for other applications. Consider the specific memory requirements for your OS, other applications, the SQL Server thread stack, and other multipage allocators. A typical formula would be `((total system memory) – (memory for thread stack) – (OS memory requirements) – (memory for other applications) – (memory for multipage allocators))`, where the memory for thread stack = `((max worker threads) (stack size))`. The stack size is 512 KB for x86 systems, 2 MB for x64 systems, and 4 MB for IA64 systems, and you can find the value for max worker threads in the max_worker_count column of sys.dm_os_sys_info.

These considerations also apply to the memory requirements for SQL Server to run in a virtual machine. Since SQL Server is designed to cache data in the buffer pool, and it will typically use as much memory as possible, it can be difficult to determine the ideal amount of RAM needed. When reducing the memory allocated to a SQL Server instance, you'll eventually reach a point where lower memory allotment gets traded for higher disk I/O access.

To configure SQL Server memory in an environment that has been over-provisioned, start by monitoring the environment and the current performance metrics, including the SQL Server Buffer Manager **page life expectancy** and **page reads/sec** and the Physical Disk **disk reads/sec** values. If the environment has excess memory, **page life expectancy** will increase by a value of one each second without any decrease under the workload, due to caching; the SQL Server Buffer Manager **page reads/sec** value will be low after the cache ramps up; and the Physical Disk **disk reads/sec** will also remain low.  

Once you understand the environment baseline, you can reduce the **max server memory** by 1 GB, then see how that impacts your performance counters (after any initial cache flushing subsides). If the metrics remain acceptable, reduce by another 1 GB, then monitor again, repeating as desired until you determine an ideal configuration.

::: moniker range="=sc-om-2016"

For more information, see [Server memory configuration options](/sql/database-engine/configure-windows/server-memory-server-configuration-options?preserve-view=true&view=sql-server-2014).

::: moniker-end
::: moniker range=">=sc-om-1801"

For more information, see [Server memory configuration options](/sql/database-engine/configure-windows/server-memory-server-configuration-options?preserve-view=true&view=sql-server-2016).

::: moniker-end

### Optimize TempDB

The size and physical placement of the tempdb database can affect the performance of Operations Manager. For example, if the size that is defined for tempdb is too small, part of the system-processing load may be taken up with autogrowing tempdb to the size required to support the workload every time you restart the instance of SQL Server.
To achieve optimal tempdb performance, we recommend the following configuration for tempdb in a production environment:

- Set the recovery model of tempdb to SIMPLE. This model automatically reclaims log space to keep space requirements small.
- Preallocate space for all tempdb files by setting the file size to a value large enough to accommodate the typical workload in the environment. It prevents tempdb from expanding too frequently, which can affect performance. The tempdb database can be set to autogrow, but this should be used to increase disk space for unplanned exceptions.
- Create as many files as needed to maximize disk bandwidth. Using multiple files reduces tempdb storage contention and yields improved scalability. However, don't create too many files as it can reduce performance and increase management overhead. As a general guideline, create one data file for each logical processor on the server (accounting for any affinity mask settings) and then adjust the number of files up or down as necessary. As a general rule, if the number of logical processors is less than or equal to 8, use the same number of data files as logical processors. If the number of logical processors is greater than 8, use eight data files and then if contention continues, increase the number of data files by multiples of 4 (up to the number of logical processors) until the contention is reduced to acceptable levels or make changes to the workload/code. If the contention isn't reduced, you may have to increase the number of data files more.  
- Make each data file the same size, allowing for optimal proportional-fill performance.  The equal sizing of data files is critical because the proportional fill algorithm is based on the size of the files. If data files are created with unequal sizes, the proportional fill algorithm tries to use the largest file more for GAM allocations instead of spreading the allocations between all the files, thereby defeating the purpose of creating multiple data files.
- Put the tempdb database on a fast I/O subsystem using solid-state drives for the most optimal performance. Use disk striping if there are many directly attached disks.
- Put the tempdb database on disks that differ from those that are used by user databases.

To configure tempdb, you can run the following query or modify its properties in Management Studio.

  ```SQL
  USE [tempdb]
  GO
  DBCC SHRINKFILE (N'tempdev' , 8)
  GO
  USE [master]
  GO
  ALTER DATABASE [tempdb] MODIFY FILE ( NAME = N'tempdev', NEWNAME = N'tempdb', SIZE = 2097152KB , FILEGROWTH = 512MB )
  GO
  ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb2', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\DATA\tempdb2.mdf' , SIZE = 2097152KB , FILEGROWTH = 512MB )
  GO
  ```

Run the T-SQL query `SELECT * from sys.sysprocesses` to detect page allocation contention for the tempdb database.  In the system table output, the wait resource may show up as "2:1:1" (PFS Page) or "2:1:3" (Shared Global Allocation Map Page). Depending on the degree of contention, this may also lead to SQL Server appearing unresponsive for short periods.  Another approach is to examine the Dynamic Management Views [sys.dm_exec_request or sys.dm_os_waiting_tasks].  The results will show that these requests or tasks are waiting for tempdb resources and have similar values as highlighted earlier when you execute the **sys.sysprocesses** query.  

If the previous recommendations don't significantly reduce the allocation contention and the contention is on SGAM pages, implement trace flag -T1118 in the Startup parameters for SQL Server so that the trace flag remains in effect even after SQL Server is recycled. Under this trace flag, SQL Server allocates full extents to each database object, thereby eliminating the contention on SGAM pages.

>[!NOTE]
> This trace flag affects every database on the instance of SQL Server.

### Max degree of parallelism

The default configuration of SQL Server for small to medium size deployments of Operations Manager is adequate for most needs.  However, when the workload of the management group scales upwards towards an enterprise class scenario (typically 2,000+ agent-managed systems and an advanced monitoring configuration, which includes service-level monitoring with advanced synthetic transactions, network device monitoring, cross-platform, and so forth) it's necessary to optimize the configuration of SQL Server described in this section of the document.  One configuration option that hasn't been discussed in previous guidance is MAXDOP.  

The Microsoft SQL Server max degree of parallelism (MAXDOP) configuration option controls the number of processors that are used for the execution of a query in a parallel plan. This option determines the computing and thread resources that are used for the query plan operators that perform the work in parallel. Depending on whether SQL Server is set up on a symmetric multiprocessing (SMP) computer, a non-uniform memory access (NUMA) computer, or hyperthreading-enabled processors, you've to configure the max degree of parallelism option appropriately.  

When SQL Server runs on a computer with more than one microprocessor or CPU, it detects the best degree of parallelism, that is, the number of processors employed to run a single statement, for each parallel plan execution.  By default, its value for this option is 0, which allows SQL Server to determine the maximum degree of parallelism.

The stored procedures and queries pre-defined in Operations Manager as it relates to the operational, data warehouse, and even audit database don't include the MAXDOP option, as there's no way during installation to dynamically query how many processors are presented to the operating system, nor does it attempt to hardcode the value for this setting, which could have negative consequences when the query is executed.  

> [!NOTE]
> The max degree of parallelism configuration option doesn't limit the number of processors that the SQL Server uses. To configure the number of processors that SQL Server uses, use the affinity mask configuration option.

- For servers that use more than eight processors, use the following configuration:
MAXDOP=8
- For servers that use eight or fewer processors, use the following configuration:
MAXDOP=0 to N
   >[!NOTE]
   > In this configuration, N represents the number of processors.
