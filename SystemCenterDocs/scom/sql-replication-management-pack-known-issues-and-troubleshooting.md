---
ms.assetid: 08ad3749-84b9-4411-8a6c-559ce5e308e6
title: Known issues and troubleshooting in Management Pack for SQL Server Replication
description: This article explains Known Issues and Troubleshooting in Management Pack for SQL Server Replication
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: troubleshooting-known-issue
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Replication

This article lists the known issues for Management Pack for SQL Server Replication.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|SQL Server Replication Database Health virtual group is empty|A SQL Server Replication Database Health virtual group may be empty in the **Summary** dashboards view even if configured SQL replications are discovered.|Create a regular group that contains MSSQL: Generic Replication Database Health class objects and restart the Operations Manager console.|
|Offline Publication and Subscription databases are not shown in the monitoring list|If Publication or Subscription databases have been set offline, these databases will be undiscovered and will not be shown in the System Center Operations Manager console. After you bring these databases online, they will be automatically rediscovered and available for monitoring.|No resolution.|
|Replication Agent State monitor fails for Pull subscriptions on SQL Server Express editions|[Applicable to SQL Server Express editions] If you select the **Run each agent at its Subscriber (pull subscriptions)** option in the **Distribution Agent Location** wizard, the **Replication Agent State** monitor will fail with errors at the Distributor replication role.|No resolution.|
|Publication discovery does not work on SQL Server 2019 CU13 and higher|If SQL Server 2019 CU13 acts as a Publisher and has one or more publications, the publication discovery will not work.|No resolution.|
