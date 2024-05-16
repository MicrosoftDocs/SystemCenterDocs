---
ms.assetid: c1f1417e-c520-4b9c-9e8c-e0bff263d311
title: Pre-Upgrade Tasks When Upgrading System Center Operations Manager
description: This guide provides the pre-upgrade tasks you must perform before attempting to upgrade to the newest release of Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 05/15/2024
ms.custom: UpdateFrequency.5, engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Pre-Upgrade tasks when upgrading to System Center Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

Perform the following pre-upgrade tasks in the order presented before you begin the upgrade process.

1. Review the Operations Manager Event Logs

2. Clean up the Database (ETL Table)

3. Configure agents to fail over between multiple gateway servers so all agents reporting to a gateway have a failover gateway assigned.   

4. Remove Agents from Pending Management

5. Disable Notification Subscriptions

6. Disable any connectors

7. Stop the Microsoft Monitoring Agent, System Center Data Access Service, System Center Configuration Management, and Microsoft Monitoring Agent services on all management servers except the one being upgraded

8. Verify that the Operational Database Has More Than 50 Percent Free Space

9. Back up the Operations Manager Databases

10. Update the agent's health service cache size temporarily to prevent loss of data while Management and Gateway servers are upgraded.

11. Stop the application pool of Operations Manager and *MonitoringViews* in IIS server.

## Review the Operations Manager event logs

Review the event logs for Operations Manager on the management servers to look for recurring warning or critical events. Address them and save a copy of the event logs before you perform your upgrade.

## Clean up the database (ETL table)

As part of upgrade to System Center Operations Manager installation (setup) includes a script to clean up ETL tables and grooming the database. However, in cases where there are a large number of rows (greater than 100,000) to clean up, we recommend running the script before starting the upgrade to promote a faster upgrade and prevent possible timeout of setup. Performing this pre-upgrade task in all circumstances ensures a more efficient installation.

### Clean up ETL

To clean up the ETL table, run the following script on the SQL Server hosting the Operations Manager database:

    
```sql
-- (c) Copyright 2004-2006 Microsoft Corporation, All Rights Reserved         --
-- Proprietary and confidential to Microsoft Corporation                      --       
-- File:      CatchupETLGrooming.sql                                          --
-- Contents: A bug in the ETL grooming code could have left the user          --
-- Database with a large amount of ETL rows to groom. This script will groom  --
-- The ETL entries in a loop 100K rows at a time to avoid filling up the      --
-- Transaction log                                                            --
--------------------------------------------------------------------------------
DECLARE @RowCount int = 1;
DECLARE @BatchSize int = 100000;
DECLARE @SubscriptionWatermark bigint = 0;     
DECLARE @LastErr int;
-- Delete rows from the EntityTransactionLog. We delete the rows with TransactionLogId that aren't being
-- used anymore by the EntityChangeLog table and by the RelatedEntityChangeLog table.
SELECT @SubscriptionWatermark = dbo.fn_GetEntityChangeLogGroomingWatermark();
WHILE(@RowCount > 0)
BEGIN
  DELETE TOP(@BatchSize) ETL  
  FROM EntityTransactionLog ETL
  WHERE NOT EXISTS (SELECT 1 FROM EntityChangeLog ECL WHERE ECL.EntityTransactionLogId = ETL.EntityTransactionLogId) AND NOT EXISTS (SELECT 1 FROM RelatedEntityChangeLog RECL
  WHERE RECL.EntityTransactionLogId = ETL.EntityTransactionLogId)
  AND ETL.EntityTransactionLogId < @SubscriptionWatermark;        
  SELECT @LastErr = @@ERROR, @RowCount = @@ROWCOUNT;            
END
```

> [!NOTE]
> Clean up of ETL can take several hours to complete.

## Remove Agents from pending management

Before you upgrade a management server, remove any agents that are in Pending Management.

1. Sign in to the Operations console by using an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2. In the **Administration** pane, expand **Device Management**, and select **Pending Management**.

3. Right-click each agent, and select **Approve** or **Reject**.

## Disable notification subscriptions

You must disable notification subscription before you upgrade the management group to ensure that notifications aren't sent during the upgrade process.

1. Sign in to the Operations console account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2. In the Operations console, select the **Administration** view.

3. In the navigation pane, expand **Administration**, expand the **Notifications** container, and select **Subscriptions**.

4. Select each subscription, and select **Disable** in the **Actions** pane.

    > [!NOTE]
    > Multiselect doesn't work when you're disabling subscriptions.

## Disable connectors

Refer to the non-Microsoft connector documentation for any installed Connectors to determine the services used for each Connector.

To stop a service for a Connector, perform the following steps:

1. On the **Start** menu, point to **Administrative Tools**, and select **Services**.

2. In the **Name** column, right-click the Connector that you want to control, and select **Stop**.

## Verify the Operations Manager database has more than 50 percent free space

You must verify that the operational database has more than 50 percent of free space before you upgrade the management group because the upgrade might fail if there isn't enough space. Ensure that the transactions logs are 50 percent of the total size of the operational database.

1. On the computer that hosts the operational database, open **SQL Server Management Studio**.

2. In the **Object Explorer**, expand **Databases**.

3. Right-click the **Operations Manager** database, select to **Reports**, **Standard Reports**, and select **Disk Usage**.

4. View the **Disk Usage** report to determine the percentage of free space.

If the database doesn't have 50 percent free space, perform the following steps to increase it for the upgrade:

1. On the computer that hosts the operational database, open **SQL Server Management Studio**.

2. In the **Connect to Server** dialog, in the **Server Type** list, select **Database Engine**.

3. In the **Server Name** list, select the server and instance for your operational database (for example, computer\INSTANCE1).

4. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.

5. In the **Object Explorer** pane, expand **Databases**, right-click the **Operations Manager** database, and select **Properties**.

6. In the **Database Properties** dialog, under **Select a page**, select **Files**.

7. In the results pane, increase the **Initial Size** value for the **MOM_DATA** database by 50 percent.

    > [!NOTE]
    > This step isn't required if free space already exceeds 50 percent.

8. Set the **Initial Size** value for the **MOM_LOG** transaction log to be 50 percent of the total size of the database. For example, if the operational database size is 100 GB, the log file size should be 50 GB. Then select **OK**.

## Back up the Operations Manager databases

Obtain verified recent backups of the operational database and of the data warehouse database before you upgrade the secondary management server. You should also create backups of databases for optional features, such as the Reporting and the Audit Collection Services database, before you upgrade them. For more information, see [Create a Full Database Backup (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

## Stop Operations Manager services on Management servers

Before upgrading the first management server in your management group, it's recommended to stop the Operations Manager services - System Center Data Access, System Center Configuration, and Microsoft Monitoring Agent on all other management servers to avoid any issues while the operational and data warehouse databases are being updated.

## Increase agent HealthService cache size

To ensure the agents can queue data during the upgrade, update the following registry setting on the agents manually or automated with your configuration management or orchestration solution:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\maximumQueueSizeKb​
```

The default value of queue size is 100 MB. It can be increased up to 1500 MB by adding or modifying the **DWORD** type registry key. ​Once you've completed the upgrade of the management group, you can reset it back to the default value.

## Next steps

To continue with the upgrade, review [Upgrade overview](deploy-upgrade-overview.md).

