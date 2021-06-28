---
ms.assetid: 08ad3749-84b9-4411-8a6c-559ce5e308e6
title: Known issues and troubleshooting in Management Pack for SQL Server
description: This article explains known issues and troubleshooting in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server

This article lists the known issues for Management Pack for SQL Server.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|Seed discovery of a deleted platform pack may continue to work on the pool nodes|An error may occur when an operating system pack was deleted, but its seed discovery is still working on the pool nodes.|Delete the corresponding seed discovery manually.|
|The status of the **Database Status** monitor is constantly changed|If the **Auto Close** parameter for the database is set to **True**, the **Database Status** monitor changes its status from **Healthy** to **Recovering/Restoring** and vice versa according to the timeout set in the override parameters.|Because of monitoring specifics, no resolution is required.|
|When you enable the **Auto Close** database parameter, performance metrics collection is blocked|If the **Auto Close** parameter is **True**, performance rules return empty values.|Set the **Auto Close** parameter to **False**.|
|If an instance monitored in agentless mode is not available, multiple errors occur in the watcher node event log|If the machine with a monitored agentless instance is not available, multiple SQL Server Monitoring MP Windows and SQL Server Discovery MP Windows errors occur in the watcher node event log. Such errors will keep coming until the machine is available.|No resolution.|
|Some issues may occur upon installation of the management pack|The log reader may begin scanning the whole SQL Server log, which may lead to triggering of all alerts found. The **RepeatCount** property may contain an excessive number of events.|No resolution.|
|Double quotes in the database name may cause database console task failures|Database console tasks take database names enclosed in double quotes as one of their arguments. A database name may contain any symbol, including double quotes. If it does, the console tasks for this database will not work.|No resolution.|
|Odd behavior of the monitors operational states|If the resource pool contains more than one management server, the operational states of all monitors will be changing according to the failover settings of the resource pool.|No resolution.|
|SQL Server on Docker: multiple errors occur after a reboot of the Docker|Multiple errors occur after a reboot of the SQL Server on Docker because Docker-ID (MachineName) is changed after the reboot.|In System Center Operations Manager, go to the monitoring template properties, open the **Service Details** tab, and click **Retry Connection**.|
|Extended discovery intervals|When using a resource pool with several watcher nodes, the discovery intervals may be significantly extended.|No resolution.|
|None of the event rules work on localized SQL DB Engines|None of the event rules works on localized SQL DB Engines. In the current implementation, these rules work with the English version only.|No resolution.|
|Console tasks do not work if names of Availability Group objects contain double-quote characters|A double-quote character cannot be used in names of Availability Groups and Databases for Always On.|No resolution.|
|Connection fails if an IP address is specified as a connection string for a Linux-based instance|When adding a Linux-based instance, connection tests fail if an IP address is specified as a connection string and the authentication type is **Windows AD credentials**.|Specify the machine name as a connection string and use the correct authentication type.|
|System Center Operations Manager issue: The Configuration Service may be frozen after Management Pack reinstallation|Configuration Service may be frozen after Management Pack reinstallation.|No resolution.|
|'Out of memory' errors are received in Operations Manager|'Out of memory' errors are regularly received, even if the server has enough memory.|Isolate the SQL Server WMI provider and increase **UploadTimeout**.|
|Errors occur in workflows related to Memory-Optimized Data databases|A "Database is being recovered. Waiting until recovery is finished." error occurs in workflows related to Memory-Optimized Data for databases with the **AutoClose** parameter set to **True**.|No resolution.|
|**Custom user policy** discovers system databases|A custom SQL Server policies may be discovered for system databases such as **master**, **msdb** etc. and custom ones. A custom user policy can be performed only on databases created by the user.|No resolution.|
|System Center Operations Manager issue: The System Center Operations Manager console may show an exception in the **Database Engines** state view if the selected instance is in the process of undiscovery|System Center Operations Manager console may show an 'object reference not set' exception in the **Database Engines** state view if the selected instance is in the process of undiscovery.|No resolution.|
|Login fails when adding a new instance using the **Add Monitoring Wizard**|The following error may appear after you finish adding a new instance to the monitoring list using the **Add Monitoring Wizard**: “An error occurred discovery: A connection was successfully established with the server, but then an error occurred during the login process.” Most likely, this error indicates that the **SQL Server MP Monitoring Pool** resource pool has not been discovered.|Decrease intervals for both the **MSSQL: Generic Monitoring Pool Watcher Discovery** discovery and the **Discover All Management Servers Pool Watcher** discovery to force them to run right away, then restore the previous value.|
|The **CPU Utilization** performance rule may show values greater than 100|Sometimes the **CPU Utilization** performance rule may show values greater than 100 due to a known issue in the 'sys.dm_os_ring_buffers' dynamic management view used by the rule to get the utilization value.|No resolution.|
|A 'Job Failed' error appears when adding a new SQL Server instance in **Add Monitoring Wizard**|On the last step of the wizard, an error message appears stating 'Job Failed'. This issue indicates that you name the monitoring template with one of the following names: **SystemCenter**, **Windows**, **System**, **SQLCorelib**.|Do not use any of the mentioned words as a monitoring template name.|
|SQL Server instances have not been discovered after importing the management pack and no alerts are raised|This may indicate that you have bound a non-basic action account to the SQL Credentials run as profile.|Configure SQL Server MP Run As Profiles.|
|The **HKTableMemoryUsageAction** workflow throws errors that are related to Memory-Optimized Data: "Memory Used By Indexes (MB)", "Memory Used By Tables (MB)"|Such errors may indicate that you have performance degradation in environments with numerous Memory-Optimized databases.|Investigate performance degradation on the affected servers.|
|Service status-related monitors do not work on SQL Server cluster instances where the SQL Server role is stopped|**SQL Server Windows Service**, **SQL Full-text Filter Daemon Launcher Service**, and **SQL Server Agent Service** monitors will be in a **Healthy** state on SQL Server cluster instances where the SQL Server role is stopped.|Due to specific behavior of cluster nodes, monitoring is not performed for SQL Server cluster instances with the disabled SQL Server role.|
|The **Primary replica** column shows different hosting machines for Availability Groups deployed on Windows and Linux-based systems|If an Availability Group is deployed on Windows and Linux-based systems under the same name, the cluster type of which is set to **External** or **None**, the discovery results for such an Availability Group will be different each time; either of the hosting machines will be shown in the **Primary replica** column. This is caused by non-unique IDs in such Availability Groups, which forces Availability Group Discovery to pick a different hosting machine during each discovery interval.|No resolution.|
|The **Dashboards** view cannot be opened on multiple management groups (System Center Operations Manager servers) targeted to the same **OperationsManagerDW** database|The **Dashboards** view is unavailable in deployments consisting of multiple management groups (System Center Operations Manager servers) that are targeted to the same **OperationsManagerDW** database.|No resolution.|
|The console task output is not produced after the execution of tasks related to SQL Server cluster instance objects.|When running tasks from the System Center Operations Manager console for any of the SQL Server cluster instance objects, the console task output is never produced and the progress wheel keeps running continuously. Even though no output is displayed and the task wizard appears to be hanging, the task being executed still can send commands to the target SQL Server cluster instance object, forcing this object to execute the command.|No resolution.|

To isolate a WMI provider, run the script below in an elevated PowerShell session:

```powershell
$a = [WMI]'Root\Microsoft\SqlServer\ComputerManagement14:__Win32Provider.name="MSSQL_ManagementProvider"'
$a.HostingModel = "NetworkServiceHost:SQL"
$a.put()
```

To revert the changes, run the following script.

```powershell
$a = [WMI]'Root\Microsoft\SqlServer\ComputerManagement14:__Win32Provider.name="MSSQL_ManagementProvider"'
$a.HostingModel = "NetworkServiceHost"
$a.put()*
```

To extend the unload timeout to 30 minutes, perform the following steps:

1. Open **WBEMTEST**.

2. Click **Connect**.

3. In the **Namespace** field, enter *Root\Microsoft\SqlServer\ComputerManagement14*, and click **Connect**.

4. Click **Query**.

5. Enter the following query.

    ```sql
    select * from __win32provider where name = 'MSSQL_ManagementProvider'
    ```

6. Click **Apply**.

7. Double-click the resulting row.

8. Double-click the **UnloadTimeout** value.

9. Select the **Not NULL** level, enter 00000000003000.000000:000, and click **Save Property**.

10. Click **Save Object**.

11. Click **Close**.