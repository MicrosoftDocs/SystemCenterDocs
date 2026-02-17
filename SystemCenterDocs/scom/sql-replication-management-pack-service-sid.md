---
ms.assetid: 71e5a3ff-147f-46d9-a195-4af43951d85e
title: Service SID in Management Pack for SQL Server Replication
description: This article explains how to configure monitoring with service SID in Management Pack for SQL Server Replication
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Service SID in Management Pack for SQL Server Replication

Management Pack for SQL Server Replication supports monitoring using Service SID. For more information on how to configure Service SID, see [Service SID in Management Pack for SQL Server](./sql-server-management-pack-service-sid.md).

In addition to the steps described in the section above, ensure to provide the following grants:

```sql
USE [msdb];
GRANT SELECT ON [dbo].[sysjobs] TO [SCOM_HealthService];
GRANT SELECT ON [dbo].[sysjobhistory] TO [SCOM_HealthService];
GRANT SELECT ON [dbo].[sysjobservers] TO [SCOM_HealthService];
GRANT SELECT ON [dbo].[MSdistpublishers] TO [SCOM_HealthService];
GRANT EXECUTE ON [dbo].[sp_help_jobactivity] TO [SCOM_HealthService];
GRANT EXECUTE ON [dbo].[agent_datetime] TO [SCOM_HealthService];
USE [master];
GRANT EXECUTE ON xp_sqlagent_enum_jobs TO [SCOM_HealthService];
```
