---
title: How and When to Clear the Cache
description: This article provides guidance on how to manage the cache for the HealthService on management servers and agents in System Center Operations Manager.
author: mgoedtel
ms.author: magoedte
manager: carmomm
ms.date: 01/04/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
ms.assetid: bea86d42-4838-46b0-96ac-75a0e8988e3c
---
# How and When to Clear the Cache
In System Center Operations Manager, when troubleshooting an issue with the Operations console or with an agent, you may see recommendations to "clear the cache." For example, see the Knowledge Base article [Troubleshooting gray agent state](http://go.microsoft.com/fwlink/p/?LinkID=200488). 

## To clear the cache

The following table explains how and when to clear the console cache or agent cache.  
  
|Cache|How to clear|When|Results|  
|---------|----------------|--------|-----------|  
|Operations console|Open the Operations console with the /clearcache parameter.<br /><br />`"C:\Program Files\Microsoft System Center 2016\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" /clearcache`|Use this method to open the Operations console if you experience errors trying to retrieve data in views, such as ObjectNotFoundExceptions, or when the cache file grows too large and you want to reduce its size on disk.|Opening the Operations console with /clearcache deletes the following file:<br /><br />%systemdrive%\Users\*username*\AppData\Local\Microsoft\Microsoft.EnterpriseManagement.Monitoring.Console\\momcache.mdb|  
|Health service on agent-managed computer|1.  In the **Monitoring** workspace, expand **Operations Manager** and then expand **Agent Details**.<br />2.  Click **Agent Health State**.<br />3.  In **Agent State**, select an agent.<br />4.  In the **Tasks** pane, click **Flush Health Service State and Cache**.|This should be the final step when troubleshooting issues with the agent, before uninstalling and reinstalling the agent.|Clearing the agent cache can cause data loss of monitoring data from that system.<br /><br />1.  Stops the Microsoft Monitoring Agent service.<br />2.  Deletes the health service store files.<br />3.  Resets the state of the agent, including all rules, monitors, outgoing data, and cached management packs.<br />4.  Starts the Microsoft Monitoring Agent service.<br /><br />When the service restarts, the agent requests configuration from its primary assigned management server. **Note:** Because this task deletes the cached data in the health service store files, including the record of this task itself, no task status is reported on completion of the task.|  
|Health service on management server|1.  In the **Monitoring** workspace, expand **Operations Manager** and then expand **Management Server**.<br />2.  Click **Management Servers State**.<br />3.  In **Management Server State**, select a management server.<br />4.  In the **Tasks** pane, click **Flush Health Service State and Cache**.|Run this task on a management server when the management server is not functional, a restart has not fixed the problem, and you have exhausted other troubleshooting options.|Clearing the agent cache can cause data loss of monitoring data from agents to the management server.<br /><br />1.  Stops the Microsoft Monitoring Agent service.<br />2.  Deletes the health service store files.<br />3.  Resets the state of the agent, including all rules, monitors, outgoing data, and cached management packs.<br />4.  Starts the Microsoft Monitoring Agent service. **Note:** Because this task deletes the cached data in the health service store files, including the record of this task itself, no task status will be reported on completion of the task.|  
  
## Next steps

- See [How to move the Operational database](manage-move-opsdb.md) to understand the sequence and steps for moving the Operations Manager operational database to a new SQL Server instance. 

- See [How to move the Reporting data warehouse database](manage-move-omdwdb.md) to understand the sequence and steps for moving the Operations Manager Reporting data warehouse database to a new SQL Server instance.

- To learn more about the default retention period for the different data types stored in the Operations Manager Reporting data warehouse database and how to modify those settings, see [How to configure grooming settings for the Operations Manager Reporting data warehouse database](manage-omdwdb-grooming-settings.md).

- To learn more about the default retention period for the different data types stored in the Operations Manager operational database and how to modify those settings, see [How to configure grooming settings for the Operations Manager database](manage-omdb-grooming-settings.md).
