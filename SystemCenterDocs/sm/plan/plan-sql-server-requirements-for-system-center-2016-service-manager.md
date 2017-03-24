---
title:  SQL Server requirements for Service Manager
description: The article describes SQL Server requirements for Service Manager.
manager:  carmonm
ms.topic:  article
ms.author: banders
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 02/02/2017
ms.technology: service-manager
ms.assetid:  26697203-df1e-4232-b9be-7c9976a362b8
---

# SQL Server requirements for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

Microsoft SQL Server hosts the databases that System Center 2016 - Service Manager creates. In addition, System Center 2016 - Service Manager requires SQL Server Analysis Services (SSAS) to work with Microsoft Online Analytical Processing (OLAP) cubes. SQL Server Reporting Services (SSRS) is required to support System Center 2016 - Service Manager reporting.

Use this information to evaluate if your SQL Server environment is ready to support the installation of or upgrade to System Center 2016. Use this information whether you are deploying one or multiple components of System Center.

## SQL Server version support

|**System Center 2016** component |SQL Server 2008 R2 SP1 Standard, Datacenter|SQL Server 2008 R2 SP2 Standard, Datacenter|SQL Server 2012 Enterprise, Standard (64-bit)|SQL Server 2012 SP1 Enterprise, Standard (64-bit)|SQL Server 2012 SP2 Enterprise, Standard (64 bit)|SQL Server 2014 Enterprise, Standard (64-bit)|SQL Server 2014 SP1 Enterprise, Standard (64-bit)|SQL Server 2014 SP2 Enterprise, Standard (64-bit)|SQL Server 2016, Enterprise, Standard  (64-bit)|
|-------------------------------------------------------------------|-----------------------------------------------|-----------------------------------------------|----------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------|----------------------------------------------------|--------------------------------------------------------|------------------------------------------------|-------------------------------------|
|**Service Manager** Database or Data Warehouse Database|||||&#8226;|&#8226;|&#8226;|&#8226;|&#8226;|
|**Service Management Automation** Web Service|||||&#8226;|&#8226;|&#8226;|&#8226;|&#8226;|

> [!NOTE]
> System Center 2016 - Service Manager requires SQL Server 2012 SP2 or later.
>
> System Center 2016 - Service Manager does not support setting the MultiSubnetFailover parameter. This parameter is not used in System Center 2016 - Service Manager connection strings.



For information about the specific versions of SQL Server that are supported in System Center 2016 - Service Manager see [Software Requirements for Service Manager](plan-software-requirements-for-system-center-2016-service-manager.md).

## Allow updates

To either install or upgrade System Center 2016 - Service Manager, computers running SQL Server that host databases must be configured to allow updates. If updates are not allowed, System Center 2016 - Service Manager Setup will not complete and the following error message will appear at the **Create database** stage of the installation:

*An error occurred while executing a customer action: _ExecuteSqlScripts. This upgrade attempt has failed before permanent modifications were made. Upgrade has successfully rolled back to the original state of the system. Once the corrections are made, you can retry upgrade for this role.*

You can check the status of **allow updates** on SQL Server by executing the following stored procedure from within SQL Server Management Studio:

```
sp_configure 'allow updates'
```

In the results table, examine the value for "run_value". If the value of "run value" is 1, set it back to 0 with the following stored procedure, and then run Setup again.

```
sp_configure 'allow updates',0 reconfigure with override
```

## AlwaysOn Availability Groups considerations for Service Manager databases

SQL Server AlwaysOn Availability Groups functionality is supported by System Center 2016 - Service Manager.

For more information about installing Service Manager with AlwaysOn availability groups, [refer here](../deploy/deploy-using-sql-server-2014-alwayson-availability-groups-with-service-manager.md).

## Next steps

- Review [Service Manager editions](plan-system-center-2016-service-manager-editions.md) to learn about the retail and select editions of Service Manager and what effect selecting the 180-day evaluation installation has on these two editions.
