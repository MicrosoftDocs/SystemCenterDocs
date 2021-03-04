---
ms.assetid: a34d3a18-0e6f-466a-b233-e6a78980962d
title: Management Pack Scope and Supported Configuration
description: This article explains how to view database and server views in Management Pack for Azure SQL Database
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Viewing Information in the Operations Console

Management Pack for Azure SQL Database provides the following views.

![Viewing Information in the Operations Console](./media/asdmp/views.png)

To find specific objects, you can use the **Scope**, **Search**, and **Find** buttons on the Operations Manager toolbar. For more information, see [Finding Data and Objects in the Operations Manager Consoles](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh212890(v=sc.12)?redirectedfrom=MSDN).

## Database Views

The following table describes views that show a databases health state.

|**View Path**|**Description**|
|-|-|
|Databases\Database State|Displays a list of monitored databases and their current states. Double-click the health state icon for a database to launch a Health Explorer window for that databases to locate monitors that affect the health state of the server and investigate any issue. The **Detail View** pane displays properties of the database selected above.|
|Performance\Database Sessions|The **Legend** pane displays a list of database sessions related counters for every monitored database. The chart illustrates information selected in the **Legend** pane.|
|Performance\Database Space|The **Legend** pane displays a list of disk space related counters for every monitored database. The chart illustrates information selected in the **Legend** pane.|
|Performance\Database Transactions|The **Legend** pane displays a list of database transactions related counters for every monitored database. The chart illustrates information selected in the **Legend** pane.|

## Server Views

The following table describes views that show a cloud services health state.

|**View Path**|**Description**|
|-|-|
|Servers\Server State|Displays a list of monitored cloud services and their current states. Double-click the health state icon for a database to launch a Health Explorer window for that databases to locate monitors that affect the health state of the server and investigate any issue. The **Detail View** pane displays properties of the database selected above.|
|Servers\Servers Diagrams|Displays a structured picture of all monitored cloud services with hosted databases. Expand the required cloud service node to drill down into hosted objects.|