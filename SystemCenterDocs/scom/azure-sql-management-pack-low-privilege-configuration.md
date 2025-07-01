---
ms.assetid: 8f864a9e-b04a-43e3-a624-574d5f08f823
title: Low-privilege configuration in Management Pack for Azure SQL Database
description: This article explains how to configure low-privilege configuration in Management Pack for Azure SQL Database
author: Anastas1ya
ms.author: v-fkornilov
manager: evansma
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Low-Privilege Configuration

This section explains how to configure low-privilege accounts to monitor the Azure SQL Database service.

To configure a low-privilege account, perform the following steps:

1. Connect to the **master** database and create server-level credentials for the low-privilege monitoring user by executing the following query:

      ```SQL
      CREATE LOGIN [MonitoringUser] WITH PASSWORD = <'YourPassword'>
      ```

2. Connect to the **master** database and map server-level credentials to the database user by executing the following query:

      ```SQL
      CREATE USER [MonitoringUser] FOR LOGIN [MonitoringUser] WITH DEFAULT_SCHEMA = sys
      ```

3. In every user database (excluding the **master** members), map server-level credentials to the database user and grant it the **VIEW DATABASE STATE** permission by executing the following query:

      Use the **MonitoringUser** value when [configuring Azure SQL Database Run As Accounts](azure-sql-management-pack-run-as-accounts.md).

      ```SQL
      CREATE USER [MonitoringUser] FOR LOGIN [MonitoringUser] WITH DEFAULT_SCHEMA = sys
      GO
      GRANT VIEW DATABASE STATE TO [MonitoringUser]
      ```
