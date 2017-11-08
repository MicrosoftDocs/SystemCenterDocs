---
ms.assetid: 5a3a8b98-1113-45bf-9484-2c807ec3d013
title: SQL Server Design Considerations
description:  This article provides detailed design guidance for SQL Server to support the Operations Manager databases and reporting component.  
author: mgoedtel
ms.author: magoedte
manager:  carmonm
ms.date: 10/02/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# SQL Server Design Considerations

System Center 2016 - Operations Manager requires access to an instance of a server running Microsoft SQL Server 2012, 2014, or SQL Server 2016 to support the operational, data warehouse, and ACS audit database. The operational and data warehouse databases are required and created when you deploy the first management server in your management group, while the ACS database is created when you deploy an ACS collector in your management group.  

In a lab environment or small-scale deployment of Operations Manager, SQL Server can be co-located on the first management server in the management group.  In a medium to enterprise-scale distributed deployment, the SQL Server instance should be located on a dedicated standalone server or in a SQL Server high-availability configuration.  In either case, SQL Server must already exist and is accessible before you start the installation of the first management server or ACS collector.  


## SQL Server requirements

The following versions of SQL Server Enterprise & Standard Edition are supported for a new or existing installation of Operations Manager to host Reporting Server, Operational, Data Warehouse, and ACS database:

* SQL Server 2016, Service Pack 1 (x64)
* SQL Server 2016 (x64)
* SQL Server 2014, Service Pack 2 (x64)
* SQL Server 2012, Service Pack 3 (x64)

> [!NOTE] 
> System Center 2016 – Operations Manager databases must use the same version of SQL Server, the [SQL Server collation setting](#sql-server-collation-setting) must be one of the following supported types as described in that section, and SQL Server Full Text Search is **required** for both the operational and data warehouse databases.  The Windows Server 2016 installation options (Server Core, Server with Desktop Experience, and Nano Server) supported by Operations Manager database components, are based on what installation options of Windows Server are supported by SQL Server.

> [!NOTE] 
> System Center 2016 – Operations Manager Reporting cannot be installed in a side-by-side fashion with the System Center Operations Manager 2012 R2 Reporting and **must** be installed in native mode only. (SharePoint integrated mode is not supported.)

Additional hardware and software considerations apply in your design planning:

-  We recommend that you run SQL Server 2012, 2014, and 2016 on computers with the NTFS file format. 
-  There must be at least 1024 MB of free disk space for the operational and data warehouse database. This is enforced at the time of database creation, and it will likely grow significantly after setup.  
-  .NET Framework 4 is required. 
-  Reporting Server is not supported on Windows Server Core.

For additional information, please see [Hardware and Software Requirements for Installing SQL Server 2014](https://msdn.microsoft.com/library/ms143506%28v=sql.120%29.aspx) or [Hardware and Software Requirements for Installing SQL Server 2016](https://msdn.microsoft.com/library/ms143506%28v=sql.130%29.aspx).  

> [!NOTE]
> During the initial installation of the operational database, only use Windows Authentication on the SQL Server that hosts the Operations Manager operational database. Do not use Mixed Mode (Windows Authentication and SQL Server Authentication) because using SQL Server Authentication mode during the initial installation of the operational database can cause issues. Although enabling Mixed Mode security is possible on the SQL Server hosting the Operations Manager operational database, it is not supported as all contact with the database is accomplished using Windows accounts only.  
> 
  
## SQL Server collation setting

The following SQL Server and Windows collations are supported by System Center 2016 - Operations Manager.  

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

Please note that if your SQL Server instance is not configured with one of the supported collations listed earlier, performing a new setup of Operations Manager setup will fail.  However, an in-place upgrade will complete successfully.  

## Firewall configuration

Operations Manager depends on SQL Server to host its databases and a reporting platform to analyze and present historical operational data.  The management server, Operations and Web console roles need to be able to successfully communicate with SQL Server, and its important to understand the communication path and ports in order to configure your environment correctly.  

If you are designing a distributed deployment that will require SQL Always On Availability Groups to provide failover functionality for the Operations Manager databases, there are additional firewall configuration settings that need to be included in your firewall security strategy.   

The following table helps you identify the firewall ports required by SQL Server that will need to be allowed at a minimum in order for server roles in your Operations Manager management group to successfully communicate. 


| Scenario | Port | Direction | Operations Manager Role | 
|-----------|---------------|---------------|---------------|
| SQL Server hosting Operations Manager databases | TCP 1433 \* | Inbound | management server and Web console (for Application Advisor and Application Diagnostics) | 
| SQL Server Browser service | UDP 1434 | Inbound | management server |
| SQL Server Dedicated Admin Connection | TCP 1434 | Inbound | management server | 
| SQL Server Always On Availability Group Listener | Administrator configured port | Inbound | management server
| SQL Server Reporting Services hosting Operations Manager Reporting Server | TCP 80 (default)/443 (SSL) | Inbound | management server and Operations console |  

\* While TCP 1433 is the standard port for the default instance of the Database Engine, if you create a named instance on a standalone SQL Server or have deployed a SQL Always On Availability Group, a custom port will be defined and should be documented for reference so that you properly configure your firewalls and enter this information during setup.      

For a more detailed overview of the firewall requirements for SQL Server, please see [Configure the Windows Firewall to Allow SQL Server Access](https://msdn.microsoft.com/library/cc646023.aspx).

## Capacity and storage considerations

### Operations Manager database

The Operations Manager database is a SQL Server database that contains all of the data needed by Operations Manager for day-to-day monitoring.  Sizing and configuration of the database server is critical to the overall performance of the management group.  The most critical resource used by the Operations Manager database is the storage subsystem, but CPU and RAM are also significant.

Factors that influence the load on the Operations Manager database include: 

- Rate of operational data collection.  Operational data consists of all the events, alerts, state changes, and performance data collected by agents.  Most of the resources that are used by the Operations Manager database are used to write this data to disk as it comes into the system.  The rate of operational data collected tends to increase as additional management packs are imported and additional agents are added.  The type of computer that an agent is monitoring is also an important factor used when determining the overall rate of operational data collection.  For example, an agent that is monitoring a business-critical desktop computer can be expected to collect less data than an agent monitoring a server that is running an instance of SQL Server with a large number of databases.
- Rate of instance space changes.  Updating this data in the Operations Manager database is costly relative to writing new operational data.  In addition, when instance space data changes, the management servers make additional queries to the Operations Manager database in order to compute configuration and group changes.  The rate of instance space changes increases as you import additional management packs into a management group.  Adding new agents to a management group also temporarily increases the rate of instance space changes.
- Number of Operations Consoles and other SDK connections running simultaneously.  Each Operations console reads data from the Operations Manager database.  Querying this data consumes potentially large amounts of storage I/O resources, CPU time, and RAM. Operations consoles that display large amounts of operational data in the Events View, State View, Alerts View, and Performance Data View tend to cause the largest load on the database.  

The Operations Manager database is a single source of failure for the management group, so it can be made highly available using supported failover configurations such as SQL Server Always On Availability Groups or Failover Cluster Instances.

### Operations Manager data warehouse database

System Center 2016 – Operations Manager inserts data into the Reporting data warehouse in near-real time, it is important to have sufficient capacity on this server that supports writing all of the data that is being collected to the Reporting data warehouse.  As with the Operations Manager database, the most critical resource on the Reporting data warehouse is the storage I/O subsystem.  On most systems, loads on the Reporting data warehouse are similar to those on the Operations Manager database, but they can vary.  In addition, the workload put on the Reporting data warehouse by reporting is different than the load put on the Operations Manager database by Operations console usage.

Factors that influence the load on the Reporting data warehouse include:

- Rate of operational data collection.  To allow for more efficient reporting, the Reporting data warehouse computes and stores aggregated data in addition to a limited amount of raw data.  Doing this extra work means that operational data collection to the Reporting data warehouse can be slightly more costly than to the Operations Manager database.  This additional cost is typically balanced by the reduced cost of processing discovery data by the Reporting data warehouse versus the Operations Manager database.
- Number of concurrent reporting users or scheduled report generation.  Because reports frequently summarize large volumes of data, each reporting user can add a significant load on the system.  The number of reports run simultaneously and the type of reports being run both affect overall capacity needs.  Generally, reports that query large date ranges or large numbers of objects require additional system resources.

Based on these factors, there are several best practices to consider when sizing the Reporting data warehouse:

- Choose an appropriate storage subsystem.  Because the Reporting data warehouse is an integral part of the overall data flow through the management group, choosing an appropriate storage subsystem for the Reporting data warehouse is very important.  As with the Operations Manager database, RAID 0 + 1 is often the best choice.  In general, the storage subsystem for the Reporting data warehouse should be similar to the storage subsystem for the Operations Manager database, and the guidance that applies to the Operations Manager database also applies to the Reporting data warehouse.
- Consider appropriate placement of data logs vs. transaction logs.  As for the Operations Manager database, separating SQL data and transaction logs is often an appropriate choice as you scale up the number of agents.  If both the Operations Manager database and Reporting data warehouse are located on the same server and you want to separate data and transaction logs, you must put the transaction logs for the Operations Manager database on a separate physical volume and disk spindles from the Reporting data warehouse to receive any benefit.  The data files for the Operations Manager database and Reporting data warehouse can share the same physical volume as long as the volume provides adequate capacity and disk I/O performance does not impeded monitoring and reporting functionality.
- Consider placing the Reporting data warehouse on a separate server from the Operations Manager database.  Although smaller-scale deployments can often consolidate the Operations Manager database and Reporting data warehouse on the same server, it is advantageous to separate them as you scale up the number of agents and the volume of incoming operational data.  This is because better reporting performance results when the Reporting data warehouse and Reporting Server are on a separate server from the Operations Manager database.

The Operations Manager data warehouse database is a single source of failure for the management group, so it can be made highly available using supported failover configurations such as SQL Server Always On Availability Groups or Failover Cluster Instances.  

## SQL Server Always On

SQL Server Always On availability groups support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted by an availability replica. 

With System Center 2016 - Operations Manager, SQL Always On is preferred over failover clustering to provide high availability for databases. All databases except the native mode Reporting Services installation, which uses two databases to separate persistent data storage from temporary storage requirements, can be hosted in an AlwaysOn Availability Group.  

To set up an availability group you'll need to deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the Operations Manager SQL Server database as an availability database.

- [Learn more](https://msdn.microsoft.com/en-us/library/ff878487.aspx) about Always On prerequisites
- [Learn more](https://msdn.microsoft.com/en-us/library/ff929171.aspx) about setting up a WSFC for Always On availability groups
- [Learn more](https://msdn.microsoft.com/en-us/library/ff878265.aspx) about setting up an availability group

### Multisubnet string

Operations Manager does not support the connection string key words (MultiSubnetFailover=True).  Because an availability group has a listener name (known as the network name or Client Access Point in the WSFC Cluster Manager) depending on multiple IP addresses from different subnets, such as when you deploy in a cross-site failover configuration, client-connection requests from management servers to the availability group listener will hit a connection timeout.  

The recommended approach to work around this when you have deployed server nodes in the availability group in a multi-subnet environment, is to do the following:

1.	Set the network name of your availability group listener to only register a single active IP address in DNS 
2.	Configure the cluster to use a low TTL value for the registered DNS record

These settings allow, when failover to a node in a different subnet, for quicker recovery and resolution of the cluster name with the new IP address.

Run the following Powershell query on any one of the SQL nodes to modify its settings.

    ```
    Import-Module FailoverClusters
    Get-ClusterResource "Cluster Name"|Set-ClusterParameter RegisterAllProvidersIP 0
    Get-ClusterResource "Cluster Name"|Set-ClusterParameter HostRecordTTL 300
    Stop-ClusterResource "Cluster Name"
    Start-ClusterResource "Cluster Name"
    ```
If you are using Always On with a listener name, you should also make these configurations changes on the listener. 

Run the following Powershell query on the SQL node currently hosting the listener to modify its settings.

    ```
    Import-Module FailoverClusters
    Get-ClusterResource <Listener Cluster Resource name> | Set-ClusterParameter RegisterAllProvidersIP 0
    Get-ClusterResource <Listener Cluster Resource name> | Set-ClusterParameter HostRecordTTL 300
    Stop-ClusterResource <Listener Cluster Resource name>
    Start-ClusterResource <Listener Cluster Resource name>
    ```

When a SQL cluster failover between different subnets occurs, you will have to restart the Operations Manager Data Access service on all your Management Servers.

## Optimizing SQL Server

In general, previous deployment experience with customers shows that performance issues are typically not caused by high resource utilization (i.e. processor or memory) with SQL Server itself; rather it is directly related to the configuration of the storage subsystem.  This is commonly attributed to not following recommended configuration guidance for the storage provisioned for the SQL Server database instance.     
Such examples are,

-  Insufficient allocation of spindles for the LUNs to support the IO requirements of Operations Manager.  
-  Hosting transaction logs and database files on the same volume.  These two workloads have very different IO and latency characteristics.
-  Configuration of TempDB is incorrect with respect to placement, sizing, etc.
-  Disk partition misalignment of volumes hosting the database transaction logs, database files, and TempDB
-  Overlooking the basic SQL Server configuration such as using AUTOGROW for database and transaction log files, MAXDOP setting for query parallelism, creating multiple TempDB data files per CPU core, etc. 

Storage configuration is one of the critical components to a SQL Server deployment for Operations Manager.  Database servers tend to be heavily I/O bound due to rigorous database read and write activity and transaction log processing.  Operations Manager’s I/O behavior pattern is typically 80% writes and 20% reads.  As a result, improper configuration of I/O subsystems can lead to poor performance and operation of SQL Server systems and becomes quite noticeable in Operations Manager.

It is very important to test the SQL Server design by performing throughput testing of the IO subsystem prior to deploying SQL Server. Make sure these tests are able to achieve your IO requirements with an acceptable latency.  Leverage the [SQLIO disk subsystem benchmarking tool](https://www.microsoft.com/download/details.aspx?id=20163) to determine the I/O capacity of the storage subsystem supporting SQL Server.  The following blog article, authored by a member of the File Server team in the product group, provides very detailed guidance and recommendations on how to go about performing stress testing using this tool with some PowerShell code, and [capturing the results using PerfMon](http://blogs.technet.com/b/josebda/archive/2013/03/28/sqlio-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares.aspx).  You can also refer to the Operations Manager Sizing Helper  for initial guidance. 

### NTFS allocation unit size

Volume alignment, commonly referred to as sector alignment, should be performed on the file system (NTFS) whenever a volume is created on a RAID device. Failure to do so can lead to significant performance degradation; these are most commonly the result of partition misalignment with stripe unit boundaries. This can also lead to hardware cache misalignment, resulting in inefficient utilization of the array cache.
When formatting the partition that will be used for SQL Server data files, it is recommended that you use a 64-KB allocation unit size (that is, 65,536 bytes) for data, logs, and tempdb. Be aware however, that using allocation unit sizes greater than 4 KB results in the inability to use NTFS compression on the volume. While SQL Server does support read-only data on compressed volumes, it is not recommended. 


### Reserve memory

Identifying the right amount of physical memory and processors to allocate to the Windows server for SQL Server 2014 and 2016 in support of System Center 2016 - Operations Manager is not an easy question to answer (not even for other workloads outside of this product for that matter).  While the sizing calculator provided by the product group, which is based off of testing performed in a lab environment that may or may not align with the typical workload and configuration in the real-world, provides guidance based on workload scale (i.e. 500 systems, 1000 systems, etc.) the integrity of what's stated is often brought into question.  It serves as an initial recommendation to start with, however it's not and cannot be considered the final configuration.   

By default, SQL Server can change its memory requirements dynamically based on available system resources. The default setting for min server memory is 0, and the default setting for max server memory is 2147483647. The minimum amount of memory you can specify for max server memory is 16 megabytes (MB).  A number of performance and memory related problems are because customer’s don’t set a value for Max. Server Memory and they don’t do that because they don’t know what to set.  A number of other factors influence the maximum amount of memory you allocate to SQL to ensure the operating system has enough memory to support the other processes running on that system, such as HBA card, management agents, anti-virus real-time scanning, etc. Otherwise, the OS and SQL will page to disk and then disk I/O increases, further decreasing performance and creating a "ripple" effect where it is noticeable in Operations Manager.  

SQL Server allows you to configure the minimum and maximum amount of memory that should be reserved and used by its process. It is recommended to specify at least 4GB of RAM as minimum amount. This should be done for every SQL node hosting one of the Operations Manager databases (Operational, Datawarehouse, ACS).

It is recommended to first start by reserving 1 GB of RAM for the OS, 1 GB for each 4 GB of RAM installed from 4–16 GB, and then 1 GB for every 8 GB RAM installed above 16 GB RAM.  Then monitor the Memory\Available MBytes performance counter in Windows to determine if you can increase the memory available to SQL Server above the starting value. (Note: This counter should remain above the 150-300 MB at a bare minimum, Windows signals the LowMemoryResourceNotification at 96MB so you want a buffer, but you should consider having it start above 1GB on larger servers with 256 GB or higher RAM). This has typically worked out well for servers that are dedicated to SQL Server.  You can also get much more technical with determining where to set 'max server memory' by working out the specific memory requirements for the OS, other applications, the SQL Server thread stack, and other multipage allocators.  Typically this would be  ((Total system memory) – (memory for thread stack) – (OS memory requirements ~ 2-4 GB) – (memory for other applications) – (memory for multipage allocations; SQLCLR, linked servers, etc.)), where the memory for thread stack = ((max worker threads) *(stack size)) and the stack size is 512 KB for x86 systems, 2 MB for x64 systems and 4 MB for IA64 systems.  The value for 'max worker threads' can be found in the max_worker_count column of sys.dm_os_sys_info.  However, the assumption with either of these methods is that you want SQL Server to use everything that is available on the machine, unless you've made reservations in the calculations for other applications. 

As more customers move towards virtualizing SQL Server in their environment, this question is more relevant in determining what is the minimum amount of memory that a SQL Server will need to run in a virtual machine.  Unfortunately there is no way to calculate what the ideal amount of memory for a given instance of SQL Server might actually be since SQL Server is designed to cache data in the buffer pool, and it will typically use as much memory as you can give it.  One of the things to keep in mind when you are looking at reducing the memory allocated to a SQL Server instance, is that you will eventually get to a point where the lower memory gets traded off for higher disk I/O access. 

If you need to figure out the ideal configuration for SQL Server memory in an environment that has been over provisioned, the best way to try to go about doing this is start off with a baseline of the environment and the current performance metrics.  Counters to begin monitoring would include: 

-  SQL Server:Buffer Manager\Page Life Expectancy 
-  SQL Server:Buffer Manager\Page reads/sec 
-  Physical Disk\Disk Reads/sec 

Typically if the environment has excess memory for the buffer pool, the Page Life Expectancy value will continue to increase by a value of one every second and it won't drop off under the workload because all of the data pages end up being cached.  At the same time, the number of SQL Server:Buffer Manager\Page reads/sec will be low after the cache ramp up occurs, which will also correspond to a low value for Physical Disk\Disk Reads/sec.  

Once you have your baseline for the environment, make a change to the sp_configure 'max server memory' option to reduce the size of the buffer pool by 1GB and then monitor the impact to the performance counters after things stabilize from the initial cache flushing that may typically occur when RECONFIGURE is run in the environment.  If the level of Page Life Expectancy remains acceptable for your environment (keeping in mind that a fixed target of >= 300 is ridiculous for servers with large amounts of RAM installed), and the number of SQL Server:Buffer Manager\Page reads/sec is within what the disk I/O subsystem can support without performance degradation, repeat the process of reducing the sp_configure value for 'max server memory' by 1GB and continuing to monitor the impact to the environment. 

You can also refer to the guidance on MSDN for [SQL 2014](https://msdn.microsoft.com/library/ms178067%28v=sql.120%29.aspx).

### Optimize TempDB

The size and physical placement of the tempdb database can affect the performance of Operations Manager.  For example, if the size that is defined for tempdb is too small, part of the system-processing load may be taken up with autogrowing tempdb to the size required to support the workload every time you restart the instance of SQL Server.
To achieve optimal tempdb performance, we recommend the following configuration for tempdb in a production environment:

-  Set the recovery model of tempdb to SIMPLE. This model automatically reclaims log space to keep space requirements small.
-  Preallocate space for all tempdb files by setting the file size to a value large enough to accommodate the typical workload in the environment. This prevents tempdb from expanding too frequently, which can affect performance. The tempdb database can be set to autogrow, but this should be used to increase disk space for unplanned exceptions.
-  Create as many files as needed to maximize disk bandwidth. Using multiple files reduces tempdb storage contention and yields significantly better scalability. However, do not create too many files because this can reduce performance and increase management overhead. As a general guideline, create one data file for each logical processor on the server (accounting for any affinity mask settings) and then adjust the number of files up or down as necessary. As a general rule, if the number of logical processors is less than or equal to 8, use the same number of data files as logical processors. If the number of logical processors is greater than 8, use 8 data files and then if contention continues, increase the number of data files by multiples of 4 (up to the number of logical processors) until the contention is reduced to acceptable levels or make changes to the workload/code. If the contention is not reduced, you may have to increase the number of data files more.  
-  Make each data file the same size; this allows for optimal proportional-fill performance.  The equal sizing of data files is critical because the proportional fill algorithm is based on the size of the files. If data files are created with unequal sizes, the proportional fill algorithm tries to use the largest file more for GAM allocations instead of spreading the allocations between all the files, thereby defeating the purpose of creating multiple data files.
-  Put the tempdb database on a fast I/O subsystem using solid state drives for the most optimal performance. Use disk striping if there are many directly attached disks.
-  Put the tempdb database on disks that differ from those that are used by user databases.

To configure tempdb, you can run the following query or modify its properties in Management Studio.

   ```
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

Run the T-SQL query SELECT * from sys.sysprocesses to detect page allocation contention for the tempdb database.  In the system table output, the waitresource may show up as "2:1:1" (PFS Page) or "2:1:3" (Shared Global Allocation Map Page). Depending on the degree of contention, this may also lead to SQL Server appearing unresponsive for short periods.  Another approach is to examine the Dynamic Management Views [sys.dm_exec_request or sys.dm_os_waiting_tasks].  The results will show that these requests or tasks are waiting for tempdb resources, and have similar values as highlighted earlier when you execute the sys.sysprocesses query.  
If the previous recommendations do not significantly reduce the allocation contention and the contention is on SGAM pages, implement trace flag -T1118 in the Startup parameters for SQL Server so that the trace flag remains in effect even after SQL Server is recycled. Under this trace flag, SQL Server allocates full extents to each database object, thereby eliminating the contention on SGAM pages. Note that this trace flag affects every database on the instance of SQL Server.


### Max degree of parallelism

The default configuration of SQL Server for small to medium size deployments of Operations Manager is adequate for most needs.  However, when the workload of the management group scales upwards towards an enterprise class scenario (typically 2,000+ agent-managed systems and an advanced monitoring configuration, which includes service-level monitoring with advanced synthetic transactions, network device monitoring, cross-platform, and so forth) it is necessary to optimize the configuration of SQL Server described in this section of the document.  One configuration option that has not been discussed in previous guidance, is MAXDOP.  

The Microsoft SQL Server max degree of parallelism (MAXDOP) configuration option controls the number of processors that are used for the execution of a query in a parallel plan. This option determines the computing and thread resources that are used for the query plan operators that perform the work in parallel. Depending on whether SQL Server is set up on a symmetric multiprocessing (SMP) computer, a non-uniform memory access (NUMA) computer, or hyperthreading-enabled processors, you have to configure the max degree of parallelism option appropriately.  
When SQL Server runs on a computer with more than one microprocessor or CPU, it detects the best degree of parallelism, that is, the number of processors employed to run a single statement, for each parallel plan execution.  By default, its value for this option is 0, which allows SQL Server to determine the maximum degree of parallelism.

The stored procedures and queries pre-defined in Operations Manager as it relates to the operational, data warehouse, and even audit database do not include the MAXDOP option, as there is no way during installation to dynamically query how many processors are presented to the operating system, nor does it attempt to hardcode the value for this setting, which could have negative consequences when the query is executed.  

> [!NOTE] 
> The max degree of parallelism configuration option does not limit the number of processors that SQL Server uses. To configure the number of processors that SQL Server uses, use the affinity mask configuration option.

-  For servers that use more than eight processors, use the following configuration: 
MAXDOP=8
-  For servers that use eight or fewer processors, use the following configuration: 
MAXDOP=0 to N
Note In this configuration, N represents the number of processors.
-  For servers that have NUMA configured, MAXDOP should not exceed the number of CPUs that are assigned to each NUMA node. 
-  For servers that have hyperthreading enabled, the MAXDOP value should not exceed the number of physical processors.
-  For servers that have NUMA configured and hyperthreading enabled, the MAXDOP value should not exceed number of physical processors per NUMA node.

You can monitor the number of parallel workers by querying sys.dm_os_tasks.  
In one customer deployment of Operations Manager 2012, which was monitoring multiple datacenter infrastructure workloads across five thousand Windows agent-managed systems, the SQL Server instance hosting the operational database exhibited significant performance degredation.  The hardware configuration of this server is a HP Blade G6 with 24 core processors and 196 GB of RAM.  The instance hosting the OperationsManager database has a MAXMEM setting of 64 GB.  After performing the suggested optimizations in this section, performance improved, however there continued to be a query parallelism bottleneck.  After testing different values, the most optimal performance was found by setting MAXDOP=4.  

### Initial database sizing

Estimating the future growth of the Operations Manager databases, specifically the operational and data warehouse databases, within the first several months after its deployment is not a simple exercise. While the Operations Manager Sizing Helper is reasonable in estimating potential growth based on the formula derived by the product group from their testing in the lab, it does not take into account serveral factors which can influence growth in the near term verus long term.  

The initial database size, as suggested by the Sizing Helper, should be allocated to its predicted size, to reduce fragmentation and corresponding overhead, which can be specified at setup time for the Operational and Data Warehouse databases. If during setup not enough storage space is available, the databases can be expanded later by using SQL Management Studio and then re-indexed thereafter to defragment and optimize accordingly. This recommendation applies also to the ACS database. 

Proactive monitoring of the growth of the operational and data warehouse database should be performed on a daily or weekly cycle.  This will be necessary to identify unexpected and significant growth spurts, and begin troubleshooting in order to determine if it is caused by a bug in a management pack workflow (i.e. discovery rule, performance or event collection rule, or monitor or alert rule) or other symptom with a management pack that was not identified during testing and quality assurance phase of the release management process.  

### Database autogrow

When the databases file size that has been reserved on disk becomes full, SQL Server can automatically increase the size, by a percentage or by a fixed amount. Moreover, a maximum database size can be configured, to prevent filling up all the space available on disk.  By default, the OperationsManager database is not configured with autogrow enabled; only the Data Warehouse and ACS databases are.  

Only rely on autogrow as a contingency for unexpected growth.  Autogrow introduces a performance penalty that should be considered when dealing with a highly transactional database.  Performance penalties include:

-  Fragmentation of the log file or database if you don’t provide an appropriate growth increment.
-  If you run a transaction that requires more log space than is available, and you have turned on the autogrow option for the transaction log of that database, then the time it takes the transaction to complete will include the time it takes the transaction log to grow by the configured amount. 
-  If you run a large transaction that requires the log to grow, other transactions that require a write to the transaction log will also have to wait until the grow operation completes.

If you combine the autogrow and autoshrink options, you might create unnecessary overhead. Make sure that the thresholds that trigger the grow and shrink operations will not cause frequent up and down size changes. For example, you may run a transaction that causes the transaction log to grow by 100 MB by the time it commits. Some time after that the autoshrink starts and shrinks the transaction log by 100 MB. Then, you run the same transaction and it causes the transaction log to grow by 100 MB again. In that example, you are creating unnecessary overhead and potentially creating fragmentation of the log file, either of which can negatively affect performance.

It is recommended to configure these two settings very carefully. The particular configuration really depends on your environment. In general, it is recommended to increase database size by a fixed amount in order to reduce disk fragmentation. See for example the following figure, where the database is configured to grow by 1024 MB each time autogrow is required.

### Cluster failover policy

Windows Server Failover Clustering is a high availability platform that is constantly monitoring the network connections and health of the nodes in a cluster.  If a node is not reachable over the network, then recovery action is taken to recover and bring applications and services online on another node in the cluster.  The default settings out of the box are optimized for failures where there is a complete loss of a server, which is considered a ‘hard’ failure.  These would be unrecoverable failure scenarios such as the failure of non-redundant hardware or power.  In these situations, the server is lost and the goal is for Failover Clustering to very quickly detect the loss of the server and rapidly recover on another server in the cluster.  To accomplish this fast recovery from hard failures, the default settings for cluster health monitoring are fairly aggressive.  However, they are fully configurable to allow flexibility for a variety of scenarios.

These default settings deliver the best behavior for most customers, however as clusters are stretched from being inches to possibly miles apart, the cluster may become exposed to additional and potentially unreliable networking components between the nodes.  Another factor is that the quality of commodity servers is constantly increasing, coupled with augmented resiliency through redundant components (such as dual power supplies, NIC teaming, and multi-path I/O), the number of non-redundant hardware failures may potentially be fairly rare.  Because hard failures may be less frequent, some customers may wish to tune the cluster for transient failures, where the cluster is more resilient to brief network failures between the nodes.  By increasing the default failure thresholds you can decrease the sensitivity to brief network issues that last a short period of time.

It is important to understand that there is no right answer here, and the optimized setting may vary by your specific business requirements and service level agreements.

### Virtualizing SQL Server

In virtual environments, for performance reasons, it is recommended that you store the operational database and data warehouse database on a direct attached storage, and not on a virtual disk. Always use Operations Manager Sizing Helper to estimate required IOPS, and stress test your data disks to verify. You can leverage the SQLIO tool for this task . 
See also [Operations Manager virtualization support](/system-center/orchestrator/system-requirements.md#virtualization) for additional guidance on virtualized Operations Manager environment.  

### Always On and recovery model

Although not strictly an optimization, an important consideration regarding Always On Availability Group is the fact that, by design, this feature require the databases to be set in the “Full” recovery model. Meaning, the transaction logs are never discarded until either a full backup is done, or only the transaction log.
For this reason, a backup strategy is not an optional but a required part of the AlwaysOn design for Operations Manager databases. Otherwise, with time, disks containing transaction logs will fill up. 

A backup strategy must take into account the details of your environment. A typical backup schedule is given in the following table.

|Backup Type | Schedule | 
|-----------|---------------|
| Transaction log only | Every one hour |
| Full | Weekly, Sunday at 3:00 AM | 

## Optimizing SQL Server reporting services 

The Reporting Services instance acts as a proxy for access to data in the Data Warehouse database. It generates and displays reports based on templates stored inside the management packs. 

Behind the scenes of Reporting Services, there is a SQL Server Database instance that hosts the ReportServer and ReportServerTempDB databases. General recommendations regarding the performance tuning of this instance apply. 

