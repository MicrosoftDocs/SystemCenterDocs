---
ms.assetid: 23bf27ad-7914-4235-a254-95c94f9f5a85
title: Known Issues and Troubleshooting in Management Pack for SQL Server Analysis Services
description: This article explains known issues and troubleshooting in Management Pack for SQL Server Analysis Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Analysis Services

This article lists the known issues for Management Pack for SQL Server Analysis Services.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|Several performance rules do not work with SSAS instances|Rules **Processing Pool I/O Job Queue length**, **Processing Pool Job Queue length**, and **Query Pool Queue length** do not work with SSAS instances on SQL Server that have cumulative update versions lower than 14.0.3015.40. The rules do not gather performance data and throw error events in the Operations Manager event log. This is caused by the wrong path to a library file in the SSAS settings stored in the Windows registry.|Install the most recent SQL Server cumulative update. If it does not help, correct the corresponding .DLL file name in the Windows registry, as described in [Correcting File Name in Windows Registry](#correcting-file-name-in-windows-registry).|
|Configuration Service may be frozen after Management Pack reinstallation|Configuration Service may be frozen after Management Pack reinstallation. This appears to be a System Center Operations Manager issue.|No resolution.|
|Errors may occur after installation of a cumulative update for SQL Server|When SQL Server is upgraded through cumulative updates, the following errors may occur: **System.InvalidOperationException: Could not Read Category Index: 13688** and **System.InvalidOperationException: The Counter layout for the Category specified is invalid, a counter of the type: AverageCount64, AverageTimer32, CounterMultiTimer, CounterMultiTimerInverse, CounterMultiTimer100Ns, CounterMultiTimer100NsInverse, RawFraction, or SampleFraction has to be immediately followed by any of the base counter types: AverageBase, CounterMultiBase, RawBase, or SampleBase**.|Restart the Microsoft Monitoring agent service (HealthService).|
|Health Service may be restarted by itself during monitoring of a large number of databases due to exceeding default thresholds for private bytes and handle count monitors|Monitoring of over 50 databases per SSAS instance can result in exceeding the default thresholds for private bytes and handle count monitors. This makes Health Service to be repeatedly restarted on agents.|Set the private bytes monitor threshold to 943718400 (default is 300 MB) and the handle count monitor threshold to 30000 (the default is 6000).|
|Non-printable characters (or formatting marks) are not supported|Management Pack for SQL Server Analysis Services does not support object names consisting of non-printable characters.|No resolution.|

## Correcting File Name in Windows Registry

To correct the corresponding .DLL file name in the Windows registry, perform the following steps:

1. Start regedit.

2. Go to HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\\MSOLAP$[instanceName]\Performance.

3. Find a key with the following value: C:\Program Files\Microsoft SQL Server\MSAS14.[instance name]\OLAP\bin\Counters\MSMDCTR\\**140.DLL**.

4. Update this key as follows: C:\Program Files\Microsoft SQL Server\MSAS14.[instance name]\OLAP\bin\Counters\\**MSMDCTR.DLL**.

5. Restart Analysis Service.