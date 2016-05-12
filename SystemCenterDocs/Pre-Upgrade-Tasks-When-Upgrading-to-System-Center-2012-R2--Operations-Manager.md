---
title: Pre-Upgrade Tasks When Upgrading to System Center 2012 R2  Operations Manager
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7518d545-fff2-45a2-93e6-f7b038fe9639
---
# Pre-Upgrade Tasks When Upgrading to System Center 2012 R2  Operations Manager
Perform the following pre\-upgrade tasks in the order presented before you begin the upgrade process.

1.  Review the [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Event Logs

2.  Cleanup the Database \(ETL Table\)

3.  Remove Agents from Pending Management

4.  Disable the Notification Subscriptions

5.  Stop the Services or Disable any Connectors

6.  Verify that the Operational Database Has More Than 50 Percent Free Space

7.  Back up the Operations Manager Databases

## Review the Operations Manager Event Logs
Review the event logs for Operations Manager on the management servers to look for recurring warning or critical events. Address them and save a copy of the event logs before you perform your upgrade.

## Cleanup the Database \(ETL Table\)
As part of upgrade to [!INCLUDE[omblue_1](Token/omblue_1_md.md)] installation \(setup\) includes a script to cleanup ETL tables, grooming the database.  However, in cases where there are a large number of rows \(greater than 100,000\) to cleanup, we recommend running the script before starting the upgrade to promote a faster upgrade and prevent possible timeout of setup. Performing this pre\-upgrade task in all circumstances ensures a more efficient installation.

Run the following query to determine the number of rows that need to be deleted from ETL and cleanup the database:

#### To Cleanup ETL

1.  To determine the number of rows that need to be deleted, run the following query:

    ```
    DECLARE @SubscriptionWatermark bigint = 0;

    SELECT @SubscriptionWatermark = dbo.fn_GetEntityChangeLogGroomingWatermark();

    Select COUNT (*)
    FROM EntityTransactionLog ETL with(nolock)
    WHERE NOT EXISTS (SELECT 1 FROM EntityChangeLog ECL with(nolock) WHERE ECL.EntityTransactionLogId = ETL.EntityTransactionLogId)
    AND NOT EXISTS (SELECT 1 FROM RelatedEntityChangeLog RECL with(nolock) WHERE RECL.EntityTransactionLogId = ETL.EntityTransactionLogId)
    AND EntityTransactionLogId < @SubscriptionWatermark;

    ```

2.  To clean up the ETL Table, run the following SQL script:

    ```
    DECLARE @RowCount int = 1;
    DECLARE @BatchSize int = 100000;
    DECLARE @SubscriptionWatermark bigint = 0;
    DECLARE @LastErr int;

    SELECT @SubscriptionWatermark = dbo.fn_GetEntityChangeLogGroomingWatermark();
    WHILE(@RowCount > 0)
    BEGIN 
    DELETE TOP (@BatchSize) ETL
    FROM EntityTransactionLog ETL
    WHERE NOT EXISTS (SELECT 1 FROM EntityChangeLog ECL WHERE ECL.EntityTransactionLogId = ETL.EntityTransactionLogId)
    AND NOT EXISTS (SELECT 1 FROM RelatedEntityChangeLog RECL WHERE RECL.EntityTransactionLogId = ETL.EntityTransactionLogId)
    AND ETL.EntityTransactionLogId < @SubscriptionWatermark;

    SELECT @LastErr = @@ERROR, @RowCount = @@ROWCOUNT;

    END
    ```

> [!NOTE]
> Cleanup of ETL can require several hours to complete.

## Remove Agents from Pending Management
Before you upgrade a management server, remove any agents that are in Pending Management.

#### To remove agents that are in Pending Management

1.  Log on to the Operations console by using an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2.  In the **Administration pane**, expand **Device Management**, and then click **Pending Management**.

3.  Right\-click each agent, and then click **Approve** or **Reject**.

## Disable the Notification Subscriptions
You should disable notification subscription before you upgrade the management group to ensure that notifications are not sent during the upgrade process.

#### To disable subscriptions

1.  Log on to the Operations console account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2.  In the Operations console, select the **Administration** view.

3.  In the navigation pane, expand **Administration**, expand the **Notifications** container, and then click **Subscriptions**.

4.  Select each subscription, and then click **Disable** in the **Actions** pane.

> [!NOTE]
> Multiselect does not work when you are disabling subscriptions.

## Stop the Services or Disable any Connectors
Refer to the non\-Microsoft connector documentation for any installed Connectors to determine the services used for each Connector.

#### To stop a service for Connectors

1.  On the **Start** menu, point to **Administrative Tools**, and then click **Services**.

2.  In the **Name** column, right\-click the Connector that you want to control, and then click **Stop**.

## Verify that the Operational Database Has More Than 50 Percent Free Space
You must verify that the operational database has more than 50 percent of free space before you upgrade the management group because the upgrade might fail if there is not enough space. You should also ensure that the transactions logs are 50 percent of the total size of the operational database.

#### To check how much free space the Operational Database has

1.  On the computer that hosts the operational database, open **SQL Server Management Studio**.

2.  In the **Object Explorer**, expand **Databases**.

3.  Right\-click the operational database, point to **Reports**, **Standard Reports**, and then click **Disk Usage**.

4.  View the **Disk Usage** report to determine the percentage of free space.

#### To increase the free space for the operational database and log files

1.  On the computer that hosts the operational database, open **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, in the **Server Type** list, select **Database Engine**.

3.  In the **Server Name** list, select the server and instance for your operational database \(for example, computer\\INSTANCE1\).

4.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.

5.  In the **Object Explorer** pane, expand **Databases**, right\-click the operational database, and then click **Properties**.

6.  In the **Database Properties** dialog box, under **Select a page**, click **Files**.

7.  In the results pane, increase the **Initial Size** value for the **MOM\_DATA** database by 50 percent.

    > [!NOTE]
    > This step is not required if free space already exceeds 50 percent.

8.  Set the **Initial Size** value for the **MOM\_LOG** to be 50 percent of the total size of the database. For example, if the operational database size is 100 GB, the log file size should be 50 GB. Then click **OK**.

## Back up the Operations Manager Databases
Obtain verified recent backups of the operational database and of the data warehouse database before you upgrade the secondary management server. You should also create backups of databases for optional features, such as the Reporting and the Audit Collection Services database before you upgrade them. For more information, see [How to: Back up a Database](http://go.microsoft.com/fwlink/p/?LinkId=220190) and [How to Schedule Backups of Operations Manager Databases](assetId:///301b7af3-3695-41b5-b91c-e1a672bce591).


