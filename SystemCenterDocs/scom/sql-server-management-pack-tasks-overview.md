---
ms.assetid: 9550f943-bcc2-45dc-a866-9eae7b3b8b0c
title: Tasks in Management Pack for SQL Server
description: This section explains tasks in the Management Pack for SQL Server
author: epomortseva
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Tasks overview

The SQL Server Management Pack provides tasks for some activities with the following targets:

- SQL Server Database Engine
- SQL Server Database
- SQL Server Agent

How to find and run the task, see [Running tasks in Operations Manager](manage-running-tasks.md).

The task can be launched for one object of the class or several at once. Tasks can be run both on Windows and Linux SQL Servers DB Engines.

System Center Operations Manager tasks require higher privileges on the agent computer and/or database to allow the task to be executed for an instance monitored in low-privilege mode. For how to give the necessary permission, see [Optional Steps for Tasks on Agents](sql-server-management-pack-low-privilege-monitoring.md#optional-steps-for-tasks-on-agents).

## List of SQL Server Database Engine tasks

- **Export Event Log**

   Export the Event log file from the selected SQL Server DB Engine with Discovery, Monitoring, and Library SQL Server MP source events. For more information, see [Export Event Log Task](sql-server-management-pack-export-event-log-task.md).

- **Global Configuration Settings**

    Shows a list of global configuration settings from a specified SQL Server from [sys.configurations](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql). The output will display a list of settings and their value.

- **Run On-Demand Database Discovery**

    Database discovery can be launched by running on-demand task without waiting for the default discovery interval. All databases will be discovered for the selected SQL Server DB Engine(s) and displayed in System Center Operations Manager in the Database view.

- **SQL Management Studio**

    Open SQL Management Studio connecting on the selected SQL Server on the instance with System Center Operations Manager.

- **SQL Profiler**

    Start a trace on the selected SQL Server by running SQL Profiler from the task on the instance with System Center Operations Manager.

- **Start SQL Agent Service from DB Engine**

   SQL Server DB Engine can be started together with SQL Server Agent by a single task from System Center Operations Manager.

- **Start SQL Full-Text filter Daemon Launcher Service**
  
   Full-Text filter Daemon Launcher Service can be started by task from System Center Operations Manager.

- **Start SQL Server Service**

    SQL Server DB Engine can be started by task from System Center Operations Manager.

- **Stop SQL Agent Service from DB Engine**

   SQL Server Agent Service can be stopped by task from System Center Operations Manager.

- **Stop SQL Full-text filter Daemon Launcher Service**
  
    Full-Text filter Daemon Launcher Service can be stopped by task from System Center Operations Manager.

- **Stop SQL Server Service**

    SQL Server DB Engine can be stopped by task from System Center Operations Manager.

> [!NOTE]
> For instance, monitored in the agentless monitoring mode only the following tasks are supported:
>
> - Global Configuration Settings
> - Run On-Demand Database Discovery
> - SQL Management Studio
> - SQL Profiler
>
> The following tasks aren't supported by SQL Server Express edition, except the SQL Server Express Edition with Advanced Services:
>
> - Start SQL Agent Service from DB Engine
> - Stop SQL Agent Service from DB Engine

## List of SQL Server database tasks

- **Check Catalog (DBCC)**

    Checks for catalog consistency within the specified database by task from System Center Operations Manager. The database must be online.

    Results options:
  - Error-none - means everything is consistency
  - Printed error message - for more information, see [DBCC CHECKCATALOG](/sql/t-sql/database-console-commands/dbcc-checkcatalog-transact-sql).
  
- **Check Database (DBCC)**

    Checks the allocation, structural, and logical integrity of all the objects in the specified database by task from System Center Operations Manager. The database must be online. The output will show a list of database objects and their state.

    For more information, see [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql).

- **Check Disk (DBCC)**

    Checks the consistency of disk space allocation structures for a specified database by task from System Center Operations Manager. The database must be online. The output will show a list of objects and their state.

    For more information, see [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql).

- **Set Database Offline**

    Make the selected databases offline by running a task from System Center Operations Manager.

- **Set Database Online**
  
    Make the selected databases online by running a task from System Center Operations Manager.

- **Set Database to Emergency State**

    Make the selected databases in the emergency state by running a task from System Center Operations Manager.

- **SQL Management Studio**

    Open SQL Management Studio connecting on the selected SQL Server on the instance with System Center Operations Manager.

- **SQL Profiler**

    Start a trace on the selected SQL Server by running SQL Profiler from the task on the instance with System Center Operations Manager.

## List of SQL Server Agent tasks

- **Run On-Demand Agent Job Discovery**

    SQL Agent job discovery can be launched by running on-demand task without waiting for the default discovery interval. All agent jobs will be discovered for the selected SQL Server Agent(s) and displayed in System Center Operations Manager in the SQL Agent Job view.

    >[!IMPORTANT]
    >To run this task, ensure that SQL Agent job discovery is enabled.

- **Start SQL Server Agent Service**

    SQL Server Agent Service can be launched by task from System Center Operations Manager.

- **Stop SQL Server Agent Service**

    SQL Server Agent Service can be stopped by task from System Center Operations Manager.
