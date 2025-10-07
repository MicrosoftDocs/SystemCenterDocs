---
ms.assetid: 23bf27ad-7914-4235-a254-95c94f9f5a85
title: Known Issues and Troubleshooting in management pack for SQL Server Analysis Services
description: This article explains known issues and troubleshooting in management pack for SQL Server Analysis Services
author: epomortseva
manager: evansma
ms.date: 04/23/2025
ms.author: v-gajeronika
ms.topic: troubleshooting-known-issue
ms.service: system-center
ms.subservice: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Analysis Services

This article lists the known issues for Management Pack for SQL Server Analysis Services.

|Issue title|Behavior/Symptom|Known workaround|
|-|-|-|
|Several performance rules don't work with SSAS instances|Rules **Processing Pool I/O Job Queue length**, **Processing Pool Job Queue length**, and **Query Pool Queue length** don't work with SSAS instances on SQL Server that have cumulative update versions lower than 14.0.3015.40. The rules don't gather performance data and throw error events in the Operations Manager event log. This is caused by the wrong path to a library file in the SSAS settings stored in the Windows registry.|Install the most recent SQL Server cumulative update. If it doesn't help, correct the corresponding .DLL file name in the Windows registry.|
|Configuration Service may be frozen after Management Pack reinstallation|Configuration Service may be frozen after Management Pack reinstallation. This appears to be a System Center Operations Manager issue.|No resolution.|
|Errors may occur after installation of a cumulative update for SQL Server|When SQL Server is upgraded through cumulative updates, the following errors may occur: **System.InvalidOperationException: Could not Read Category Index: 13688** and **System.InvalidOperationException: The Counter layout for the Category specified is invalid, a counter of the type: AverageCount64, AverageTimer32, CounterMultiTimer, CounterMultiTimerInverse, CounterMultiTimer100Ns, CounterMultiTimer100NsInverse, RawFraction, or SampleFraction has to be immediately followed by any of the base counter types: AverageBase, CounterMultiBase, RawBase, or SampleBase**.|Restart the Microsoft Monitoring agent service (HealthService).|
|Health Service may be restarted by itself during monitoring of a large number of databases due to exceeding default thresholds for private bytes and handle count monitors|Monitoring of over 50 databases per SSAS instance can result in exceeding the default thresholds for private bytes and handle count monitors. This makes Health Service to be repeatedly restarted on agents.|Set the private bytes monitor threshold to 943718400 (default is 300 MB) and the handle count monitor threshold to 30000 (the default is 6000).|
|The **Service State** monitor doesn't work on a clustered SQL Server Analysis Services instance|The **Service State** monitor doesn't work when the SQL Server Analysis Services server is used as a cluster instance.|No resolution.|
|The console task output isn't produced after the execution of tasks related to SQL Server objects|System Center Operations Manager console shows no output in the **Task Status** dialog and the progress wheel keeps running continuously. Even though no output is produced and the task wizard appears to stop responding, the task being executed can still send commands to the target SQL Server instance object, forcing this object to execute the requested command. Task execution results are available in the **Task Status** view, which can be found in the System Center Operations Manager console.|No resolution.|

To correct the corresponding .DLL file name in the Windows registry, follow these steps:

1. Start regedit.

2. Go to HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\\MSOLAP$[instanceName]\Performance.

3. Find a key with the following value: C:\Program Files\Microsoft SQL Server\MSAS14.[instance name]\OLAP\bin\Counters\MSMDCTR\\**140.DLL**.

4. Update this key as follows: C:\Program Files\Microsoft SQL Server\MSAS14.[instance name]\OLAP\bin\Counters\\**MSMDCTR.DLL**.

5. Restart Analysis Service.
