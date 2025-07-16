---
title: SQL Server requirements for Service Manager
description: The article describes SQL Server requirements for Service Manager.
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.subservice: service-manager
ms.assetid: 26697203-df1e-4232-b9be-7c9976a362b8
ms.custom: UpdateFrequency.5, engagement-fy24
---

# SQL Server requirements for System Center - Service Manager

Microsoft SQL Server hosts the databases that System Center - Service Manager creates. In addition, System Center - Service Manager requires SQL Server Analysis Services (SSAS) to work with Microsoft Online Analytical Processing (OLAP) cubes. SQL Server Reporting Services (SSRS) is required to support System Center - Service Manager reporting.

Use this information to evaluate if your SQL Server environment is ready to support the installation of or upgrade to System Center. Use this information whether you're deploying one or multiple components of System Center.

## SQL Server version support

::: moniker range="sc-sm-2016"

|**System Center 2016** component |SQL Server 2008 R2 SP1 Standard, Datacenter|SQL Server 2008 R2 SP2 Standard, Datacenter|SQL Server 2012 Enterprise, Standard (64-bit)|SQL Server 2012 SP1 Enterprise, Standard (64-bit)|SQL Server 2012 SP2 Enterprise, Standard (64 bit)|SQL Server 2014 Enterprise, Standard (64-bit)|SQL Server 2014 SP1 Enterprise, Standard (64-bit)|SQL Server 2014 SP2 Enterprise, Standard (64-bit)|SQL Server 2016, Enterprise, Standard  (64-bit)|
|-------------------------------------------------------------------|-----------------------------------------------|-----------------------------------------------|----------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------|----------------------------------------------------|--------------------------------------------------------|------------------------------------------------|-------------------------------------|
|**Service Manager** Database or Data Warehouse Database||||||&#8226;|&#8226;|&#8226;|&#8226;|
|**Service Management Automation** Web Service||||||&#8226;|&#8226;|&#8226;|&#8226;|

> [!NOTE]
> System Center 2016 - Service Manager requires SQL Server 2014 or later.
>
> System Center 2016 - Service Manager doesn't support setting the MultiSubnetFailover parameter. This parameter isn't used in System Center 2016 - Service Manager connection strings.

For detailed information about the requirements for Service Manager components, see [Software Requirements](sm-software-reqs.md).

::: moniker-end

::: moniker range="sc-sm-2019"

| **System Center 2019 component**                      | **Service Manager** Database or Data Warehouse Database | 
|-------------------------------------------------------|---------------------------------------------------------|
| **SQL Server 2014 Enterprise, Standard (64-bit)**     | Yes                                                       |
| **SQL Server 2014 SP1 Enterprise, Standard (64-bit)** | Yes                                                       |
| **SQL Server 2014 SP2 Enterprise, Standard (64-bit)** | Yes                                                       |
| **SQL Server 2016, Enterprise, Standard (64-bit)**    | Yes                                                       |
| **SQL Server 2017 and Cumulative Updates**    | Yes                                                       |
| **SQL Server 2019 with Cumulative Update 8 (CU8) or later**    | Yes                                                       |

>[!NOTE]
> - Service Manager 2019 supports SQL 2019 with CU8 or later; however, it doesn't support SQL 2019 RTM.
> - Use ODBC 17.3 to 17.10.4.1, and MSOLEDBSQL 18.2 to 18.6.6.

For detailed information about the requirements for Service Manager components, see [Software Requirements](sm-software-reqs.md).
::: moniker-end

::: moniker range="sc-sm-2022"

| **System Center 2022 component**                      | **Service Manager** Database or Data Warehouse Database |
|-------------------------------------------------------|---------------------------------------------------------|
| **SQL Server 2017 and Cumulative Updates**    | Yes                                                       |
| **SQL Server 2019 with Cumulative Update 8 (CU8) or later**    | Yes                                                       |
| **SQL Server 2022**                                     | Yes                                                       |

>[!NOTE]
> - Use ODBC 17.3 to 17.10.4.1, and MSOLEDBSQL 18.2 to 18.6.6.

For detailed information about the requirements for Service Manager components, see [Software Requirements](sm-software-reqs.md).

::: moniker-end

::: moniker range="sc-sm-2025"

| **System Center 2025 component**                      | **Service Manager** Database or Data Warehouse Database |
|-------------------------------------------------------|---------------------------------------------------------|
| **SQL Server 2017 and Cumulative Updates**    | Yes                                                       |
| **SQL Server 2019 with Cumulative Update 8 (CU8) or later**    | Yes                                                       |
| **SQL Server 2022**                                     | Yes                                                       |

>[!NOTE]
> - Use ODBC 17.3 to 17.10.6, and MSOLEDBSQL 18.2 to 18.7.2.

For detailed information about the requirements for Service Manager components, see [Software Requirements](sm-software-reqs.md).

::: moniker-end


## Allow updates

To either install or upgrade System Center - Service Manager, computers running SQL Server that host databases must be configured to allow updates. If updates aren't allowed, System Center - Service Manager Setup won't complete and the following error message appears at the **Create database** stage of the installation:

*An error occurred while executing a customer action: _ExecuteSqlScripts. This upgrade attempt has failed before permanent modifications were made. Upgrade has successfully rolled back to the original state of the system. Once the corrections are made, you can retry upgrade for this role.*

You can check the status of **allow updates** on SQL Server by executing the following stored procedure from within SQL Server Management Studio:

```
sp_configure 'allow updates'
```

In the results table, examine the value for **run_value**. If the value of **run value** is 1, set it back to 0 with the following stored procedure, and then run Setup again.

```
sp_configure 'allow updates',0 reconfigure with override
```

## AlwaysOn Availability Groups considerations for Service Manager databases

SQL Server AlwaysOn Availability Groups functionality is supported by System Center - Service Manager.

For more information about installing Service Manager with AlwaysOn availability groups, [refer here](sql-always-on.md).

## Next steps

To learn about the retail and select editions of Service Manager and what effect selecting the 180-day evaluation installation has on these two editions, review [Service Manager editions](sm-editions.md).
