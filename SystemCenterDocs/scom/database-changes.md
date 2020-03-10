---
ms.assetid: 9c962b3f-8695-4da7-ab16-e152eef1ab2d
title: Change databases for gMSA in System Center Operations Manager
description: This article provides information on how to create users, assign roles, and membership to the group Managed Service Accounts (gMSA), a new feature supported in Operations Manager 2019 UR1.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 02/04/2020
ms.prod: system-center
monikerRange: 'sc-om-2019'
ms.technology: operations-manager
ms.topic: article
---

# Change databases

This article provides information on how to create users, assign roles, and membership to group Managed Service Accounts (gMSAs).

>[!NOTE]
>This article applies to System Center 2019 Update Rollup 1 (UR1) Operations Manager.

These roles are similar to the roles created for non-gMSA accounts.

## Action account

**System databases: msdb**

1. In the SQL Server Management Studio, go to **Databases** \>**System Databases** \> **msb** \> **Security** \> **Users**.

1. Create a new user.

1. Select **Windows user** in the **User type** box.

1. Select **Entire Directory** in the **From the location** box. Select **Service Accounts** in the **Object types** box.

    ![Server management object types](media/gmsa/server-management-object-types.png)

1. Check names for *momActGMSA*, which is an example gMSA for the Action account, in the directory.
Because *momActGMSA* is an example, use the name of the gMSA that you intend to use as the Action account.

   ![Server management select user](media/gmsa/server-management-select-users.png)


1. Assign the following roles for the Action account:

   - SQLAgentOperatorRole
   - SQLAgentReaderRole
   - SQLAgentUserRole
   
   ![Database user membership](media/gmsa/database-user-membership.png)


Follow steps 1 to 5 from the previous procedure. Assign the roles by using the information in this table.

| Database|Roles|
|---------|---------|
|    **Action account**     |         |
| Operations Manager |db\_datareader, db\_datawriter, db\_ddladmin, dbmodule\_users|
|   **Data Access Service account**       |         |
|   Systems Database: msdb |SQLAgentOperatorRole, SQLAgentReaderRole, SQLAgentUserRole |
|Operations Manager DB |  configsvc\_users, db\_accessadmin, db\_datareader,  db\_datawriter, db\_ddladmin, db\_securityadmin, dbmodule\_users, sdk\_users, sql\_dependency\_subscriber|
| OperationsManager DW|apm\_datareader, db\_datareader, OpsMgrReader |
|  **Data Writer account** |         |
|   Operations Manager DB| apm\_datareader, apm\_datawriter,  db\_datareader, dwsynch\_users|
|OperationsManager DW|apm\_datareader, db\_datareader, db\_owner, OpsMgrWriter|
|   **Data Reader account** |         |
|     System Databases: master|      RSExecRole   |
| System Databases: msdb| RSExecRole, SQLAgentOperatorRole,  SQLAgentReaderRole, SQLAgentUserRole|
| OperationsManager DW |apm\_datareader, db\_datareader, OpsMgrReader|
|  Report Server Database      | db\_owner,  RSExecRole      |
|  Report Server Temp Database       | db\_owner, RSExecRole      |

## Next steps
  [Service-level changes](service-level-changes.md)
