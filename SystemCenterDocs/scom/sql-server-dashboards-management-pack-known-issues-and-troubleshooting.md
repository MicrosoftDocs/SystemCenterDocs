---
ms.assetid: 603255c8-723e-46ce-b1fc-7d127b37ebd6
title: Known issues and troubleshooting in Management Pack for SQL Server Dashboards
description: This article explains the known issues and troubleshooting in Management Pack for SQL Server Dashboards
author: vchvlad
ms.author: v-vchernov
manager: evansma
ms.date: 11/22/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Dashboards

This article lists the known issues for Management Pack for SQL Server Dashboards.

|Issue title|Behavior/Symptom|Known workaround|
|-|-|-|
|Signed SQL Server Dashboards aren't saved if the default management pack is removed|Signed SQL Server Dashboards store changes in Microsoft.SystemCenter.OperationsManager.DefaultUser.|Import the default management pack.|
|Obsolete data is displayed|The Operations Manager database should be synchronized with Data Warehouse. If the default synchronization procedure hasn't been executed for a long period of time, dashboards can't get the most recent data.|Restart the System Center Data Access service and perform other required actions to reactivate delta synchronization.|
|The Operations Manager console crashes if the System Center Operations Manager server is unavailable|If the Operations Manager console loses connection with the System Center Operations Manager server, SQL Server Dashboards may crash. It can happen due to network issues or System Center Operations Manager server issues (for example, if the console is left unattended over a long period of time).|Check the connection with the server and reopen the Operations Manager console.|
|Only the last modification is applied if the SQL Server Dashboards configuration is being edited by several operators simultaneously|When a user edits SQL Server Dashboard from the Operations Manager console and Web console simultaneously, the “Last changes apply” algorithm is applied.|Reopen the dashboard or wait until the data is refreshed.|
|The Operations Manager console is unresponsive after failures occur when saving the configuration|In some cases, System Center Operations Manager is unable to save the updated dashboard configuration. In this case, dialogs on SQL Server Dashboards become unresponsive. The user can find error details in Application event log.|Reopen the Operations Manager console.|
|Objects are displayed with the **Not monitored** state|When more than 1000 objects are discovered simultaneously (and the discovery process isn't finished), all objects may have the **Not monitored** state.|Wait until the data is refreshed.|
|Alerts are displayed with the 0 value|When more than 5000 objects are discovered simultaneously (and the discovery process isn't finished), the alerts will be displayed with the 0 value.|Wait until the data is refreshed.|
|No remote changes of Silverlight version of Operations Manager are received|Any changes made in Silverlight version of the Operations Manager console from a remote workstation may not be saved.|Reopening the dashboard or reloading the console is ineffective. To apply changes, access the console directly.|
|Usage of some special Windows themes may lead to a crash of the Operations Manager console|Some changes in Windows the color scheme (for example, changing of foreground text color to another color) may lead to a crash of the Operations Manager console.|Use standard Windows themes and text colors.|
|Procedures aren't deleted from data warehouse storage|Stored procedures may remain in data warehouse storage even after Microsoft Windows Group Policy Management Pack was uninstalled.|Uninstall Microsoft Windows Group Policy Management Pack and remove stored procedures manually.|
|Timeouts issues|When working with the dashboard, especially when processing large data volumes, a user may face a situation when processes can't be completed within the preset timeout.|Timeout values for queries execution in Datawarehouse DB may be set by the user manually via the server registry. The user can create the HKLM\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Data Warehouse key and add the REG_DWORD type value with the Search Command Timeout Seconds name. The server will use this value instead of default 180 seconds.|
|Display problems may occur when working with groups in the web version of the Operations Manager console|A problem with displaying add/delete forms may occur while using a Silverlight web version of the Operations Manager console: the form text may be loaded before the form itself if the Dashboard contains eight or more groups.|No resolution.|
|Problems may occur when working with older versions of the management pack|The following versions of Management Pack for SQL Server are deprecated: 6.1.314.35, 6.1.400.0, 6.3.173.0, 6.3.173.1, 6.4.0.0, 6.4.1.0, 6.5.1.0, 6.5.4.0, 6.6.0.0, 6.6.2.0, 6.6.3.0.|Use up-to-date versions of the management pack (starting from version 6.6.4.0).|
|Dashboards may crash after upgrade|After the dashboards are upgraded to version 6.6.7.30 or higher, the Operations Manager console may crash with the **ObjectNotFoundException** error.|Wait until the importing process is complete and restart the Operations Manager console.|
|Colors in Microsoft Silverlight may be assigned incorrectly|Combo box colors and the main ScrollViewer background may be displayed incorrectly, especially when using the dark theme.|No resolution.|
|Various issues may appear during rapid changes performed in the datacenter view|If the user rapidly changes datacenter dashboard views while the loader is displayed, the last selected view can still be opened, but the queries of the previously closed views aren't canceled.|No resolution.|
|Dashboards may get stuck while loading|When there are more than 50 K objects on a dashboard monitored by multi-instance performance collection rules, Datawarehouse DB statistics may get broken and the Dashboard loading time could get longer than usual. Moreover, extensive TempDB and Log space usage (~2-5 GB) can be noticed.|Wait until the Dashboard is loaded, then run the **sp_updatestats** stored procedure in Datawarehouse DB.|
|Outdated group names are displayed in the instance view|If a group is renamed or renamed groups are present in System Center Operations Manager, the old group names may be displayed in SQL Server dashboards instance view. If some groups are renamed in System Center Operations Manager after importing the dashboards, the old names may still be displayed.|No resolution.|
|Users with limited access may not see SQL instances on the SQL Server Roles dashboard|If a user is assigned to a limited access role (for example, with access to SSAS Instance group, SSRS Instance Group, and SQL Server DB Engine Group only), no SQL instances are visible on SQL Server Roles dashboard.|As long as SQL Server Roles dashboard is based on Server Roles Group, the user should obtain access to Server Roles Group to make SQL instances visible on the dashboard.|
|No animation on the datacenter view dashboard|When the datacenter view dashboard is refreshed using the refresh button from the dropdown menu, no animation is shown.|No resolution.|
|Distributed applications added to the datacenter view show **No States**|When adding a distributed application to the main dashboards view, it appears as **No States**.|SQL Dashboards can work with objects that belong to groups, even when **Add Virtual Group** is used. A distributed application may not have any group. To solve the issue, create a new group and add distributed applications to this group.|
|The discrepancy in the number of objects monitored of the selected class in the **System Center Operations Manager console** Summary Dashboards view|The **System Center Operations Manager console** Summary Dashboards view may show a different number of monitored objects, such as deleted objects as well, as compared with the **Web console** Dashboards due to the synchronization lag between the Operations Manager and the Data Warehouse databases.|Use the [Web console Dashboards](sql-server-dashboards-management-pack-sql-server-dashboards.md).|
