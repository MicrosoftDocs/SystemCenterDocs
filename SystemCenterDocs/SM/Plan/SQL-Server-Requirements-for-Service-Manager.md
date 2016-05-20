---
title: SQL Server Requirements for Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26697203-df1e-4232-b9be-7c9976a362b8
---
# SQL Server Requirements for Service Manager
Microsoft® SQL Server® hosts the databases that [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] creates. In addition, [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] requires SQL Server Analysis Services \(SSAS\) to work with Microsoft Online Analytical Processing \(OLAP\) cubes. SQL Server Reporting Services \(SSRS\) is required to support [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)]reporting.

All SQL Server requirements are listed at [SQL Server](http://go.microsoft.com/fwlink/?LinkId=268329) and SQL Server editions are listed at [Operating System and Database Edition Support](http://go.microsoft.com/fwlink/?LinkId=268324).

> [!NOTE]
> [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] 2012 with no service pack is supported on SQL Server 2008 R2 without a service pack. [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] 2012 SP1 requires SQL Server 2008 R2 SP1 or later.
> 
> [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] does not support setting the MultiSubnetFailover parameter. This parameter is not used in [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] connection strings.

## SQL Server 2012 Standard and Enterprise Editions
SQL Server 2012 is available in Standard, Enterprise, and Business Intelligence editions. [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] will function with all editions. However, there are additional features available in SQL Server 2012 Enterprise that can enhance your experience with the [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] data warehouse:

-   **Analysis Services Files**: In the Enterprise and Business Intelligence editions of SQL Server 2012, you can decide where Analysis Services database files will be stored. In the Standard edition, there is only one default location for the files.

-   **Cube Processing**: In the Enterprise and Business Intelligence editions, cubes are processed incrementally each night. In the Standard edition, the entire cube is processed each night and therefore, the amount of processing time required will increase as more data is accumulated. Cubes can still be queried when being processed however, reporting performance will be reduced.

-   **Measure Group Partitions**: In the Enterprise and Business Intelligence editions, measure groups are partitioned on a monthly basis, instead of as one large partition. This reduces the amount of time it takes to process the partition.

-   **PowerPivot**: In the Enterprise and Business Intelligence editions, you can use Microsoft SQL Server PowerPiviot for SharePoint.

You must make your decision to use either the Standard, Enterprise, or Business Intelligence editions of SQL Server 2012 before you install [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)]. It is possible to use a combination of editions for the [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] database and use a different edition for the data warehouse databases.

For more information comparing SQL Server editions, see [SQL Server 2012 Editions](http://go.microsoft.com/fwlink/p/?LinkId=259487).

> [!NOTE]
> [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] was tested using the Standard and Enterprise editions of SQL Server 2012.

For information about the specific versions of SQL Server that are supported in [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] see [Software Requirements for Service Manager](Software-Requirements-for-Service-Manager.md).

## SQL Server 2008 R2 Standard and Enterprise Editions
SQL Server 2008 R2 is available in both Standard and Enterprise editions. [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] will function with both editions. However, there are additional features available in SQL Server 2008 Enterprise that can enhance your experience with the [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] data warehouse:

-   **Analysis Services Files**: In the Enterprise edition of SQL Server 2008, you can decide where Analysis Services database files will be stored. In the Standard edition, there is only one default location for the files.

-   **Cube Processing**: In the Enterprise edition, cubes are processed incrementally each night. In the Standard edition, the entire cube is processed each night and therefore, the amount of processing time required will increase as more data is accumulated. Cubes can still be queried when being processed however, reporting performance will be reduced.

-   **Measure Group Partitions**: In the Enterprise edition, measure groups are partitioned on a monthly basis, instead of as one large partition. This reduces the amount of time it takes to process the partition.

-   **PowerPivot**: In the Enterprise edition, you can use Microsoft SQL Server PowerPiviot for SharePoint.

You must make your decision to use either the Standard or Enterprise editions of SQL Server 2008 before you install [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)]. It is possible to use SQL Server 2008 Standard for the [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] database and use SQL Server 2008 Enterprise for the data warehouse databases.

For more information comparing SQL Server editions, see [Microsoft SQL Server 2008 Enterprise and Standard Feature Compare](http://go.microsoft.com/fwlink/?LinkId=242074). \(Adobe Reader is required.\)

> [!NOTE]
> [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] was tested using both the Standard and Enterprise editions of SQL Server 2008. No other editions of SQL Server are supported.

For information about the specific versions of SQL Server that are supported in [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] see [Software Requirements for Service Manager](Software-Requirements-for-Service-Manager.md).

## Allow Updates
To either install or upgrade [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)], computers running SQL Server that host databases must be configured to allow updates. If updates are not allowed, [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] Setup will not complete and the following error message will appear at the **Create database** stage of the installation:

"An error occurred while executing a customer action: \_ExecuteSqlScripts. This upgrade attempt has failed before permanent modifications were made. Upgrade has successfully rolled back to the original state of the system. Once the corrections are made, you can retry upgrade for this role."

You can check the status of **allow updates** on SQL Server by executing the following stored procedure from within SQL Server Management Studio:

```
sp_configure 'allow updates'
```

In the results table, examine the value for "run\_value". If the value of "run value" is 1, set it back to 0 with the following stored procedure, and then run Setup again.

```
sp_configure 'allow updates',0 reconfigure with override
```

## AlwaysOn Availability Groups Considerations for Service Manager Databases
SQL Server AlwaysOn Availability Groups functionality is supported by all versions of [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] for the default server instance. However, SQL AlwaysOn Availability Groups functionality is not supported for a named instance.

When considering SQL Server AlwaysOn Availability Groups for the Service Manager database or the DWDataMart, you should determine whether availability replica should support either or both of the following active\-secondary capabilities:

-   Read\-only connection access which enables read\-only connections to the replica to access and read its databases when it is running as a secondary replica.

-   Performing backup operations on its databases when it is running as a secondary replica.

[!INCLUDE[crabout](Token/crabout_md.md)] installing Service Manager with AlwaysOn availability groups on [TechNet](http://blogs.technet.com/b/babulalghule/archive/2013/02/17/how-to-install-service-manager-2012-sp1-with-a-sql-2012-alwayson-availability-groups.aspx).

[!INCLUDE[crabout](Token/crabout_md.md)] AlwaysOn Availability Groups, see [AlwaysOn Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).


