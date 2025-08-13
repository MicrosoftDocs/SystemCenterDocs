---
ms.assetid: 
title: Tasks in Management Pack for SQL Server Analysis Services
description: This section explains tasks in the Management Pack for SQL Server Analysis Services
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---
# Overview of SQL Server Analysis Services Management Pack tasks

The SQL Server Analysis Services Management Pack provides tasks for some activities with the target Instance:

- **Export Event Log**

   Export the Windows Event log file from the machine hosting SQL Server Analysis Services instance.
   The exported source events with ID 4221 are:

  - SQL Server Analysis Services MP Library
  - SQL Server Analysis Services Discovery MP
  - SQL Server Analysis Services Monitoring MP
  - SQL Server MP Default

   For more information, see [Export Event Log Task](sql-server-management-pack-export-event-log-task.md).

- **Start Analysis Services**

    SQL Server Analysis Services instance can be started by task from System Center Operations Manager.

- **Stop Analysis Services**

    SQL Server Analysis Services instance can be stopped by task from System Center Operations Manager.
