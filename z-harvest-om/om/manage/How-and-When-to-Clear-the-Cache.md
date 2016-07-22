---
title: How and When to Clear the Cache
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bea86d42-4838-46b0-96ac-75a0e8988e3c
author:mgoedtel
manager:cfreemanwa
---
# How and When to Clear the Cache
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], when troubleshooting an issue with the Operations console or with an agent, you may see recommendations to "clear the cache". \(For example, see the Knowledge Base article [Troubleshooting gray agent state](http://go.microsoft.com/fwlink/p/?LinkID=200488).\) The following table explains how and when to clear the console cache or agent cache.  
  
|Cache|How to clear|When|Results|  
|---------|----------------|--------|-----------|  
|Operations console|Open the Operations console with the \/clearcache parameter.<br /><br />`"C:\Program Files\System Center Operations Manager 2012\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" /clearcache`|Use this method to open the Operations console if you experience errors trying to retrieve data in views, such as ObjectNotFoundExceptions, or when the cache file grows too large and you want to reduce its size on disk.|Opening the Operations console with \/clearcache deletes the following file:<br /><br />%systemdrive%\\Users\\*username*\\AppData\\Local\\Microsoft\\Microsoft.EnterpriseManagement.Monitoring.Console\\momcache.mdb|  
|Health service on agent\-managed computer|1.  In the **Monitoring** workspace, expand **Operations Manager** and then expand **Agent Details**.<br />2.  Click **Agent Health State**.<br />3.  In **Agent State**, click an agent.<br />4.  In the **Tasks** pane, click **Flush Health Service State and Cache**.|This should be the final step when troubleshooting issues with the agent, before uninstalling and reinstalling the agent.|Clearing the agent cache can cause data loss of monitoring data from that system.<br /><br />1.  Stops the System Center Management service.<br />2.  Deletes the health service store files.<br />3.  Resets the state of the agent, including all rules, monitors, outgoing data, and cached management packs.<br />4.  Starts the System Center Management service.<br /><br />When the service restarts, the agent requests configuration from the management server. **Note:** Because this task deletes the cached data in the health service store files, including the record of this task itself, no task status will be reported on completion of the task.|  
|Health service on management server|1.  In the **Monitoring** workspace, expand **Operations Manager** and then expand **Management Server**.<br />2.  Click **Management Servers State**.<br />3.  In **Management Server State**, click a management server.<br />4.  In the **Tasks** pane, click **Flush Health Service State and Cache**.|Run this task on a management server when the management server is not functional, a restart has not fixed the problem, and you have exhausted other troubleshooting options.|Clearing the agent cache can cause data loss of monitoring data from agents to the management server.<br /><br />1.  Stops the System Center Management service.<br />2.  Deletes the health service store files.<br />3.  Resets the state of the agent, including all rules, monitors, outgoing data, and cached management packs.<br />4.  Starts the System Center Management service. **Note:** Because this task deletes the cached data in the health service store files, including the record of this task itself, no task status will be reported on completion of the task.|  
  
## See Also  
[Maintenance of Operations Manager](../../om/manage/Maintenance-of-Operations-Manager.md)  
[Monitoring the Health of the Management Group](../../om/manage/Monitoring-the-Health-of-the-Management-Group.md)  
[Inventory of Operations Manager Infrastructure](../../om/manage/Inventory-of-Operations-Manager-Infrastructure.md)  
[Scheduling Maintenance in Operations Manager](../../om/manage/Scheduling-Maintenance-in-Operations-Manager.md)  
[How to Configure Grooming Settings for the Reporting Data Warehouse Database](../../om/manage/How-to-Configure-Grooming-Settings-for-the-Reporting-Data-Warehouse-Database.md)  
[How to Restart a Management Server](../../om/manage/How-to-Restart-a-Management-Server.md)  
[How to Configure Grooming Settings for the Operations Manager Database](../../om/manage/How-to-Configure-Grooming-Settings-for-the-Operations-Manager-Database.md)  
[Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](../../om/manage/Recommendations-for-Daily--Weekly--and-Monthly-Operations-Manager-Tasks.md)  
  
