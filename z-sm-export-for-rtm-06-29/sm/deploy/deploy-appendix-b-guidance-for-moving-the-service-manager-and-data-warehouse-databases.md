---
title: Appendix B - Guidance for Moving the Service Manager and Data Warehouse Databases
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b6c406a-7cb3-4be7-902b-5a09be71ad98
---

# Appendix B - Guidance for Moving the Service Manager and Data Warehouse Databases

After you have deployed Service Manager, you might need to move the Service Manager or data warehouse databases from one computer running Microsoft SQL Server to another for reasons such as the following:  

-   You need to replace hardware that is experiencing issues and that is no longer considered reliable.  

-   You need to add additional hardware to improve scalability and performance.  

-   You need to move a database and log file to a different volume because of space or performance reasons.  

-   You need to change hardware that is leased and is due to expire soon.  

-   You need to change or upgrade hardware to comply with new hardware standards.  

-   You initially installed multiple Service Manager components on a single server, and you need to distribute some components to other servers.  

-   You need to restore functionality in a failure scenario.  

 If you want the move the data warehouse database, and if you have installed Service Manager within the last 90 days, it might be easier for you to unregister the data warehouse, install a new data warehouse, and register the new database. If the data has not been groomed from the Service Manager database, there will be no data loss in the data warehouse database because it will be synchronized. By default, the grooming interval for work items is 90 days from the last time a work item was modified.&nbsp;Using this process is much simpler than using the following guidance, which details how to move your databases from one server to another and requires many steps.  

## Moving databases  
 For procedures about how to move databases from one computer running SQL Server to another, see the following topics:  

-   [Moving the Service Manager Database](../../../sm/deploy/deploy-guide/Moving-the-Service-Manager-Database.md)  

     Describes how to move the Service Manager database from one computer running SQL Server to a new computer running SQL Server.  

-   [Moving Data Warehouse Databases](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md)  

     Describes how to move Service Manager data warehouse databases to new computers running SQL Server.  

## See also  

-   [System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  

-   [Operations Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)  

-   [Administrator's Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  

-   [Planning Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)
