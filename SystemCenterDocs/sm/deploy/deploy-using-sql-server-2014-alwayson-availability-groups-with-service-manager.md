---
description:  
manager:  cfreeman
ms.topic:  article
author:  bandersmsft
ms.author: banders
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-10-12
title:  Using SQL Server 2014 AlwaysOn availability groups with Service Manager
ms.technology:  service-manager
ms.assetid:  706e433d-c641-4dc3-8be5-fe582ef9f4bc
---

# Using SQL Server 2014 AlwaysOn availability groups with Service Manager

>Applies To: System Center 2016 - Service Manager

The information in this topic provides tasks that you need to perform in order for Service Manager to work effectively when using availability groups. It also emphasizes specific SQL Server 2014 AlwaysOn functionality that Service Manager 2016 supports.

However, this information is not intended to provide detailed instructions on how to configure a SQL Server 2014 AlwaysOn Availability Group. Additionally, Service Manager does not support setting the MultiSubnetFailover parameter. This parameter is not used in Service Manager connection strings.

>[!IMPORTANT]
Service Manager does not support a topology where the reporting and analysis server database is configured as part of the AlwaysOn Availability Group.

## SQL Server 2014 AlwaysOn supported Service Manager databases

SQL 2014 Server AlwaysOn supports the following Service Manager databases:

- Service Manager CMDB
- Service Manager Data Warehouse (all 3 databases)
- OM and CM DataMart

## New management group installation

Use the following tasks when you install a new management group with a SQL 2014 AlwaysOn availability group.

### Before installing Service Manager on an availability group

1. Ensure that you use the Group Listener Name and port when installing Service Manager for the databases that are going to be added to the availability databases.
2. The first management server will use the Group Listener to get the primary SQL instance, and will install the databases on that instance.

### After installing the first management server

1. Ensure that the recovery model of the database is full. Open **SQL Server Management Studio** and connect to the instance where the database(s) are installed. Right-click the targeted database, and select its  **properties**  and then select  **Options**. If the recovery model is not listed as **Full** , then select  **Full**  from the drop-down list.
2. Create a full back up the databases.
3. Use SQL Server Management Studio to add the databases to the availability databases. When adding the databases to the availability databases under  **Select Data Synchronization**, three choices are possible:  **Full** ,  **Join only**  and  **Skip initial data synchronization**. Choose the option that is most appropriate for you. We recommend selecting  **Full**  and allowing the  **Add Database wizard**  to create a full backup and restore of the databases on the secondary replicas. More steps might or might not be needed depending on which choice you made. See  [Manually Prepare a Secondary Database for an Availability Group (SQL Server)](https://msdn.microsoft.com/library/ff878349.aspx) for more information.

## Use an existing management group

Service Manager setup allows you to install SQL Always on with the default instance name or with single instance name. It doesn't provide the flexibility to have multiple instance names. This limitation is with a new installation of Service Manager, but all SQL AlwaysOn options work without any problem when you migrate a database (including SQL AlwaysOn with a failover clustering instance (FCI)).


Use the following series of tasks when using an existing management group with a SQL Server 2014 AlwaysOn availability group.

1. Prepare SQL Server AlwaysOn setup separately. You might also consider SQL Server AlwaysOn with an FCI.
2. Create an availability group listener(AGL) and choose an appropriate port number. Avoid the default port 1433. For example: AGL name = SMListener and AGL Port = 5122
3. Open the inbound port for the SQL Server instance and AGL on each computer running SQL Server.
4. Review the information at [Moving the Service Manager Database](deploy-moving-the-service-manager-database.md)  and follow the steps there, with the following changes:
    1. In step 5, *To Configure Service Manager tables*, use the `AGL Name,AGL Port number` instead of the computer name hosting the Service Manager database, for example: SMListener,5122
    2. In Step 6, use the `AGL Name,AGL Port number` to update the both DWStaging and Config database tables.
    3. In Step 7, *Configure the registry on all the management servers*, change the registry key `HKEY\_LOCAL\_MACHINE\Software\Microsoft\System Center2010\Common\Database` and give `DatabaseServerName` as `AGL Name,AGL Port number`.

To summarize, you are changing the computer name hosting the Service Manager database to *AGL Name*,*AGL Port number* for SQL Server AlwaysOn support.
