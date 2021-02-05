---
ms.assetid: 08ad3749-84b9-4411-8a6c-559ce5e308e6
title: Known Issues and Troubleshooting
description: This article explains Known Issues and Troubleshooting
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting

This article lists the known issues for Management Pack for SQL Server.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|Seed discovery of a deleted platform pack may continue to work on the pool nodes|An error may occur when an operating system pack was deleted, but its seed discovery is still working on the pool nodes.|Upon deletion of an operating system pack, delete the corresponding seed discovery manually.|
|**Database Status** monitor constantly changes its status|If the **Auto Close** parameter for the database is set to **True**, the **Database Status** monitor changes its status from **Healthy** to **Recovering/Restoring** and vice versa according to the timeout set in the override parameters.|Because of monitoring operation specifics, no resolution is required.|
|Enabling of the **Auto Close** database parameter blocks performance metrics collection|If the **Auto Close** parameter for a database is set to **True**, performance rules return empty values for this database.|Set th **Auto Close** parameter back to **False**.|
|If a machine containing a monitored agentless instance is not available, multiple errors occur in the watcher node event log|If a machine containing a monitored agentless instance is not available, multiple SQL Server Monitoring MP Windows and SQL Server Discovery MP Windows errors occur in the watcher node event log. Such errors will keep coming until the machine is available.|No resolution.|
|Some issues may occur upon installation of the management pack|The log reader may begin scanning the whole SQL Server log, which may lead to triggering of all alerts found. At that, the **RepeatCount** property may contain an excessive number of events.|No resolution.|
|Double quotes in a database name may cause database console tasks failures|Database console tasks take database names enclosed in double quotes as one of their arguments. A database name may contain any symbol, including double quotes. If it does, the console tasks for this database will not work.|No resolution.|
|Odd behavior of the monitors operational states|If the resource pool contains more than one management server, the operational states of all monitors will be changing according to the failover settings of the resource pool.|No resolution.|
|SQL Server on Docker: multiple errors occur after a reboot of the Docker|Multiple errors occur after a reboot of the SQL Server on Docker because Docker-ID (MachineName) is changed after the reboot.|In SCOM, go to the monitoring template properties, open the **Service Details** tab and click **Retry Connection**.|
|Extended discovery intervals|When using a resource pool with several watcher nodes, the discovery intervals may be significantly extended.|No resolution.|
|None of the event rules works on localized SQL DB Engines|None of the event rules works on localized SQL DB Engines. In the current implementation, these rules work with the English version only.|No resolution.|
|Console tasks for Availability Group objects with names containing a double-quote character do not work|a double-quota character  cannot be used in names of Availability Group and Databases in the Availability Group (for Always On). Therefore, console tasks for objects with such names do not work.|No resolution.|
|Connection fails when an IP address is specified as a connection string for a Linux-based instance|When adding a Linux-based instance (**Add Instances** step of the **Add Monitoring Wizard**), the connection test fails if the IP address is specified as a connection string and the authentication type is **Windows AD credentials**.|Specify the machine name as a connection string and use the correct authentication type.|
|SCOM issue: Configuration Service may be frozen after Management Pack re-installation|Configuration Service may be frozen after Management Pack re-installation.|No resolution.|
|“Out of memory” errors are received in the Operations Manager|“Out of memory” errors are regularly received in the Operations Manager while the server has plenty of memory.|Isolate the SQL Server WMI provider and increase the UploadTimeout. See [Isolating SQL Server WMI Provider](#isolating-sql-server-wmi-provider).|
|Errors occur in workflows related to Memory-Optimized Data databases|The following errors occur in workflows related to Memory-Optimized Data for databases with the **AutoClose** parameter set to **True**: "Database is being recovered. Waiting until recovery is finished."|No resolution.|
|The **Custom user policy** discovery discovers system databases|The discovery may discover custom SQL Server policies for system databases (such as “master”, “msdb” etc.) and custom ones. In fact, a custom user policy can be performed only databases created by the user.|No resolution.|
|SCOM issue: Sometimes SCOM console may show an exception in the **Database Engines** state view if the selected instance is in the process of undiscovery|Sometimes SCOM console may show an "object reference not set" exception in the **Database Engines** state view if the selected instance is in the process of undiscovery.|No resolution.|
|Login fails when adding a new instance using the **Add Monitoring Wizard**|The following error may appear after you finish adding a new instance to the monitoring using the **Add Monitoring Wizard**: “An error occurred discovery: A connection was successfully established with the server, but then an error occurred during the login process.” Most likely, this error indicates that the **SQL Server MP Monitoring Pool** resource pool has not yet been discovered.|Decrease intervals for both the **MSSQL: Generic Monitoring Pool Watcher Discovery** discovery and the **Discover All Management Servers Pool Watcher** discovery to force them to run right away, then restore the previous value.|
|The **CPU Utilization** performance rule may show values greater than 100|Sometimes the **CPU Utilization** performance rule may show values greater than 100. This occurs due to a known issue in the sys.dm_os_ring_buffers dynamic management view used by the rule to get the utilization value.|No resolution.|
|A “Job Failed” error appears when adding a new SQL Server instance to monitoring with **Add Monitoring Wizard**|On the last step of the wizard, an error message appears that states “Job Failed.” This most likely indicates that you name the monitoring template with one of the following names: **SystemCenter**, **Windows**, **System**, **SQLCorelib**.|Do not use any of the mentioned words as a monitoring template name.|
|SQL Server instances have not been discovered after importing the management pack and configuring it, and no alerts have been raised|This may indicate that you have bound a non-basic action account to the SQL Credentials run as profile.|Configure the SQL Server MP Run As Profiles.|
|Errors occur in the **HKTableMemoryUsageAction** workflow related to Memory-Optimized Data: "Memory Used By Indexes (MB)", "Memory Used By Tables (MB)"|Such errors may indicate that you have performance degradation in the environments with a lot of Memory-Optimized databases|Investigate performance degradation on affected servers and solve it if possible.|
|Service-status related monitors does not work on SQL Server cluster instances where the SQL Server role is stopped|**SQL Server Windows Service**, **SQL Full-text Filter Daemon Launcher Service** and **SQL Server Agent Service** monitors will be in a **Healthy** state on SQL Server cluster instances where the SQL Server role is stopped.|Due to specific behavior of cluster nodes, monitoring is not performed for SQL Server cluster instances with the disabled SQL Server role.|
|The **Primary replica** column shows different hosting machines for Availability Groups that are deployed on Windows and Linux-based systems under the same name and with the **External** or **None** cluster type|If an Availability Group is deployed on Windows and Linux-based systems under the same name, the cluster type of which is set to **External** or **None**, the discovery results for such an Availability Group will be different each time and will be showing either of the hosting machines in the **Primary replica** column, one after another. This is caused by non-uniqueness of IDs of such Availability Groups and forces Availability Group Discovery to pick a different hosting machine during each discovery interval and show this machine as a source.|No resolution.|
|The **Dashboards** view cannot be opened on multiple management groups (SCOM servers) targeted to the same OperationsManagerDW database|The **Dashboards** view is unavailable in deployments consisting of multiple management groups (SCOM servers) that are targeted to the same **OperationsManagerDW** database.|No resolution.|
|Non-printable characters (or formatting marks) are not supported|Management Pack for SQL Server does not support object names consisting of non-printable characters.|No resolution.|

## Isolating SQL Server WMI Provider

To isolate the provider in its own host, run the script below in an elevated PowerShell session:

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

3. In the **Namespace** field, enter *Root\Microsoft\SqlServer\ComputerManagement14* and click **Connect**.

4. Click **Query**.

5. Enter the following query.

    ```sql
    select * from __win32provider where name = 'MSSQL_ManagementProvider'
    ```
6. Click **Apply**.

7. Double-click the resulting row.

8. Double-click the **UnloadTimeout** value.

9. Select the **Not NULL** level, enter 00000000003000.000000:000 and click **Save Property**.

10. Click **Save Object**.

11. Click **Close**.