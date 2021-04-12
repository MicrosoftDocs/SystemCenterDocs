---
ms.assetid: f79efcef-1dae-4a9a-a079-f6e8378070f9
title: Security Configuration in Management Pack for SQL Server Replication
description: This article explains security configuration in Management Pack for SQL Server Replication
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Security Configuration in Management Pack for SQL Server Replication

This section explains how to configure security for Management Pack for Microsoft SQL Server Replication.

## Run As Profiles

Management Pack for Microsoft SQL Server Replication uses the same Run As profiles as Management Pack for SQL Server. For more information, see [SQL Server Run As Profiles](sql-server-management-pack-run-as-profiles.md).

>[!NOTE]
>Using Service Security Identifier (SID) or Local System account as the Run As account is not supported in this management pack.

## Low-Privilege Agent Monitoring

To configure low-privilege monitoring, in addition to the steps described in [Low-Privilege Agent Monitoring](sql-server-management-pack-low-privilege-monitoring.md), perform the following steps on an agent machine:

1. Open SQL Server Management Studio and connect to the SQL Server Database Engine instance that participates in Replication.

2. Create the **SQLMPLowPriv** user in each user database and **master**, **msdb** and **model** databases.

3. Grant the **SQLMPLowPriv** user the following permissions on both the **Distributor** and the **Publisher** SQL Server Replication roles:
  
    ```SQL
    USE [msdb]
    GO
    GRANT SELECT ON [dbo].[MSdistpublishers] TO [SQLMPLowPriv]
    GRANT EXECUTE ON [dbo].[agent_datetime] TO [SQLMPLowPriv]
    ```
  
4. Grant the **SQLMPLowPriv** user the following permissions on the **Subscriber** SQL Server Replication role:

    ```SQL
    USE [msdb]
    GO
    GRANT EXECUTE ON [dbo].[agent_datetime] TO [SQLMPLowPriv]
    ```

5. In SQL Server Management Studio, add the **SQLMPLowPriv** user to the **db_owner** database role for each distribution database on the **Distributor** SQL Server Replication role. In cases of multiple distributor databases, this permission should be granted to each database:

    ```SQL
    USE [distribution]
    GO
    ALTER ROLE [db_owner] ADD MEMBER [SQLMPLowPriv]
    ```

6. In SQL Server Management Studio, add the **SQLMPLowPriv** user to the **db_owner** database role for each database that participates in publication on the **Publisher** SQL Server Replication role. In cases of multiple publication databases, this permission should be granted to each database:

    ```SQL
    /*Run this query on databases that participate in Publication.
    Replace the 'DatabaseName' parameter with the value that you want to use.*/
    USE [DatabaseName]
    GO
    ALTER ROLE [db_owner] ADD MEMBER [SQLMPLowPriv]
    ```

7. In SQL Server Management Studio, add the **SQLMPLowPriv** user to the **db_owner** database role for each database that participates in subscription on the **Subscriber** SQL Server Replication role. In cases of multiple subscription databases, this permission should be granted to each database:

    ```SQL
    /*Run this query on databases that participate in Subscription.
    Replace the 'DatabaseName' parameter with the value that you want to use.*/
    USE [DatabaseName]
    GO
    ALTER ROLE [db_owner] ADD MEMBER [SQLMPLowPriv]
    ```