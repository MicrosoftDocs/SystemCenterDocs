---
title: Using SQL Server AlwaysOn availability groups with Service Manager
description: Use SQL Server AlwaysOn availability groups with Service Manager to support a failover environment.
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: 706e433d-c641-4dc3-8be5-fe582ef9f4bc
ms.custom: UpdateFrequency2, engagement-fy24
---

# Use SQL Server AlwaysOn availability groups with Service Manager to support failover



The information in this article provides tasks that you need to perform in order for Service Manager to work effectively when using availability groups. AlwaysOn supports a failover environment. This information is supported only with SQL Server 2012 SP2 and above.

However, this information isn't intended to provide detailed instructions on how to configure a SQL Server AlwaysOn Availability Group. Additionally, Service Manager doesn't support setting the MultiSubnetFailover parameter. This parameter isn't used in Service Manager connection strings.

>[!IMPORTANT]
> Service Manager doesn't support a topology where the reporting and analysis server database is configured as part of the AlwaysOn Availability Group.

> [!NOTE]
> After deploying Service Manager on the SQL server nodes participating in SQL Always On, to enable [CLR strict security](/sql/database-engine/configure-windows/clr-strict-security), run the [SQL script](system-requirements.md#enable-clr-strict-security) on each Service Manager database.

## SQL Server AlwaysOn supported Service Manager databases

SQL Server AlwaysOn supports the following Service Manager databases:

- Service Manager CMDB
- Service Manager Data Warehouse (all the three databases)
- OM and CM DataMart

## New management group installation

Use the following tasks when you install a new management group with a SQL AlwaysOn availability group.

### Before installing Service Manager on an availability group

1. Ensure that you use the Group Listener Name and port when installing Service Manager for the databases that are going to be added to the availability databases.
2. The first management server will use the Group Listener to get the primary SQL instance and will install the databases on that instance.

### After installing the first management server

1. Ensure that the recovery model of the database is full. Open **SQL Server Management Studio** and connect to the instance where the database(s) are installed. Right-click the targeted database, and select its **properties**  and then select  **Options**. If the recovery model isn't listed as **Full** , then select  **Full**  from the dropdown list.
2. Create a full backup of the databases.
3. Use SQL Server Management Studio to add the databases to the availability databases. When adding the databases to the availability databases under  **Select Data Synchronization**, three choices are possible:  **Full** ,  **Join only**  and  **Skip initial data synchronization**. Choose the option that is most appropriate for you. We recommend selecting  **Full**  and allowing the  **Add Database wizard**  to create a full backup and restore of the databases on the secondary replicas. More steps might or might not be needed depending on which choice you made. For more information, see [Manually Prepare a Secondary Database for an Availability Group (SQL Server)](/sql/database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server).

## Use an existing management group

Use the following series of tasks when using an existing management group with a SQL Server AlwaysOn availability group.

1. Prepare SQL Server AlwaysOn setup separately. You might also consider SQL Server AlwaysOn with an FCI.
2. Create an availability group listener(AGL) and choose an appropriate port number. Avoid the default port 1433. For example: AGL name = SMListener and AGL Port = 5122
3. Open the inbound port for the SQL Server instance and AGL on each computer running SQL Server.
4. Review the information at [Move the Service Manager and data warehouse databases](move-databases.md#move-the-service-manager-database)  and follow the steps there, with the following changes:
    1. In step 5, *To Configure Service Manager tables*, use the `AGL Name,AGL Port number` instead of the computer name hosting the Service Manager database, for example: SMListener,5122
    2. In Step 6, use the `AGL Name,AGL Port number` to update both DWStaging and Config database tables.
    3. In Step 7, *Configure the registry on all the management servers*, change the registry key `HKEY\_LOCAL\_MACHINE\Software\Microsoft\System Center2010\Common\Database` and give `DatabaseServerName` as `AGL Name,AGL Port number`.

To summarize, you're changing the computer name hosting the Service Manager database to *AGL Name*,*AGL Port number* for SQL Server AlwaysOn support.

## Next steps

- To create a system image that contains the software needed for use as a template so that you can apply it to new servers, review [Create and deploy server images of Service Manager](deploy-sm-images.md).
