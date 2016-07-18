---
title: How to Restart a Management Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35142d1f-9771-46ea-a3ba-014f0a904593
author:mgoedtel
manager:cfreemanwa
---
# How to Restart a Management Server
Sometimes you need to restart a [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] management server, such as when you update the operating system. To reduce the impact on your monitoring activities, follow these guidelines:  
  
-   When your management group has only one management server, do not place the management server in maintenance mode before restarting. Schedule the restart for a time when you expect the least activity, such as after business hours.  
  
-   When your management group has more than one management server:  
  
    -   Restart half or fewer management servers at one time.  
  
    -   Place the management servers to be restarted in maintenance mode before restarting. Maintenance mode will initiate failover of workloads to other management servers in the resource pool. After the server is restarted, remove it from maintenance mode.  
  
When maintenance mode is not used, after the server is restarted, you might seem some availability alerts for the server. The alerts will close automatically after the server is running again.  
  
## See Also  
[Maintenance of Operations Manager](../../om/manage/Maintenance-of-Operations-Manager.md)  
[Monitoring the Health of the Management Group](../../om/manage/Monitoring-the-Health-of-the-Management-Group.md)  
[Inventory of Operations Manager Infrastructure](../../om/manage/Inventory-of-Operations-Manager-Infrastructure.md)  
[Scheduling Maintenance in Operations Manager](../../om/manage/Scheduling-Maintenance-in-Operations-Manager.md)  
[How and When to Clear the Cache](../../om/manage/How-and-When-to-Clear-the-Cache.md)  
[How to Configure Grooming Settings for the Reporting Data Warehouse Database](../../om/manage/How-to-Configure-Grooming-Settings-for-the-Reporting-Data-Warehouse-Database.md)  
[How to Configure Grooming Settings for the Operations Manager Database](../../om/manage/How-to-Configure-Grooming-Settings-for-the-Operations-Manager-Database.md)  
[Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](../../om/manage/Recommendations-for-Daily--Weekly--and-Monthly-Operations-Manager-Tasks.md)  
  
