---
title: How to Configure Grooming Settings for the Reporting Data Warehouse Database
description: This article reviews the default grooming settings for the Reporting data warehouse database and how to modify those settings.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 12/05/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 8dfd8f03-85ac-4231-8861-1d98e354cf94
---

# How to configure grooming settings for the Reporting data warehouse database

The Reporting data warehouse stores data for a specified length of time, depending on the data (Alert, State, Event, Aem, or Performance) and the aggregation type (raw data, hourly aggregations, daily aggregations).  The database is set up to delete older data in order to maintain performance by managing its size.  Deleting the older data is called **grooming**.  
  
The following table highlights the default data types and retention period after initial setup of the data warehouse database.

| Dataset | Aggregation Type| Retention Period (in days) |
|-----------|---------------|---------------|
| Alert | Raw | 400 | 
| Client Monitoring | Raw | 30 |
| Client Monitoring | Daily | 400 | 
| Events | Raw | 100 | 
| Performance | Raw | 10 | 
| Performance | Hourly | 400 |
| Performance | Daily | 400 | 
| State | Raw | 180 | 
| State | Hourly | 400 | 
| State | Daily | 400 | 
  
Settings for grooming the data warehouse can be changed through Microsoft SQL Server Management Studio.  
  
## To change grooming settings in the Reporting data warehouse  
  
1.  Log on to the computer with an account that is a member of the SQL Server sysadmin fixed server role.

2.  On the Start Page, type **SQL Server Management Studio** and the program will appear.  Click the program to open SQL Server Management Studio.  You might want to right-click the program and pin it to the Start Page.
  
3.  In the **Connect to Server** dialog box, in the **Server Type** list, select **Database Engine**; in the **Server Name** list, select the server and instance for your Reporting data warehouse (for example, computer\INSTANCE1); in **Authentication** list, select **Windows Authentication**; and then click **Connect**.  
  
4.  In the Object Explorer pane, expand **Databases**, expand **OperationsManagerDW**, and then expand **Tables**.  
  
5.  Right-click **dbo.Dataset,** and then click **Open Table**.  
  
6.  Locate the dataset for which you want to change the grooming setting in the **DatasetDefaultName** column and make note of its GUID in the **DatasetId** column.  
  
7.  In the Object Explorer pane, right-click **dbo.StandardDatasetAggregation** and then click **Open Table**.  
  
8.  In the **DatasetId** column, locate the dataset GUID you noted in step 5. Multiple entries of the same GUID might display.  
  
9.  Locate the aggregation type from the list in the **AggregationTypeId** column by using the following values:  
  
    -   0 = raw, nonaggregated data  
  
    -   10 = subhourly  
  
    -   20 = hourly  
  
    -   30 = daily  
  
After you have located the dataset and its aggregation type, scroll to the **MaxDataAgeDays** column, and then edit the value there to set the grooming interval.  
  
## Next steps

To learn more about the default retention period for the different data types stored in the Operations Manager operational database and how to modify those settings, please see
[How to configure grooming settings for the Operations Manager database](manage-omdb-grooming-settings.md).
  
