---
title: How to Configure Grooming Settings for the Operations Manager Database
description: This article reviews the default grooming settings for the operational database and how to modify those settings.
author: mgoedtel
ms.author: magoedte
manager: cfreeman
ms.date: 11/10/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: ccbc61b1-4919-4514-ac2e-ea68384e3be8
---

# How to configure grooming settings for the Operations Manager database

The grooming process removes unnecessary data from the Operations Manager database in order to maintain performance by managing its size.  You can configure the grooming setting for the following data types:  
  
-   Resolved alerts  
  
    > [!NOTE]  
    > Active alerts are never groomed. You must close an alert before it will be groomed.  
  
-   Event data  
  
-   Performance data  
  
-   Task history  
  
-   Monitoring job data  
  
-   State change events data  
  
-   Performance signature  
  
-   Maintenance mode history  
  
-   Availability history  
  
Any updates to the grooming settings are applied immediately.  
  
Use the following procedure to specify when specific data types are deleted or groomed from the Operations Manager database in a management group. The default grooming setting for all data types is data older than 7 days.  
  
## To configure database grooming settings for a management group  
  
1.  In the Operations console, click **Administration**.  
  
2.  In the navigation pane, expand **Administration**, and then click **Settings**.  
  
3.  In the **Settings** pane, right-click **Database Grooming**, and then click **Properties**.  
  
4.  In the **Global Management Group Settings - Database Grooming** dialog box, select a data type, and then click **Edit**.  
  
5.  In the dialog box for the record type, specify **Older than** days, and then click **OK**.  
  
6.  In the **Global Management Group Settings - Database Grooming** dialog box, select another data type to **Edit** or click **OK**.  
  
## Next steps

- To learn more about the default retention period for the different data types stored in the Operations Manager Reporting data warehouse database and how to modify those settings, please see [How to configure grooming settings for the Operations Manager Reporting data warehouse database](How-to-Configure-Grooming-Settings-for-the-Reporting-Data-Warehouse-Database.md).


  
