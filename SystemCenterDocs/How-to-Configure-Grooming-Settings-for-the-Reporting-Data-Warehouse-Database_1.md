---
title: How to Configure Grooming Settings for the Reporting Data Warehouse Database_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8231e5bb-1674-426f-ab98-f4a1a25ccd77
---
# How to Configure Grooming Settings for the Reporting Data Warehouse Database_1
The Reporting data warehouse stores data for a specified length of time, depending on the data \(Alert, State, Event, Aem, or Performance\) and the aggregation type \(raw data, hourly aggregations, daily aggregations\).  The database is set up to delete older data. Deleting the older data is called **grooming**.

The following table shows the default retention settings for the different types of data.

|Data Set|Aggregation Type|Days To Be Kept|
|------------|--------------------|-------------------|
|Alert|Raw data|400|
|State|Raw data|180|
|State|Hourly aggregations|400|
|State|Daily aggregations|400|
|Event|Raw data|100|
|Aem|Raw data|30|
|Aem|Daily aggregations|400|
|Perf|Raw data|10|
|Perf|Hourly aggregations|400|
|Perf|Daily aggregations|400|

Settings for grooming the data warehouse can be changed through Microsoft SQL Server Management Studio.

### To change grooming settings in the Reporting data warehouse

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, in the **Server Type** list, select **Database Engine**; in the **Server Name** list, select the server and instance for your Reporting data warehouse \(for example, computer\\INSTANCE1\); in **Authentication** list, select **Windows Authentication**; and then click **Connect**.

3.  In the Object Explorer pane, expand **Databases**, expand **OperationsManagerDW**, and then expand **Tables**.

4.  Right\-click **dbo.Dataset,** and then click **Open Table**.

5.  Locate the dataset for which you want to change the grooming setting in the **DatasetDefaultName** column and make note of its GUID in the **DatasetId** column.

6.  In the Object Explorer pane, right\-click **dbo.StandardDatasetAggregation** and then click **Open Table**.

7.  In the **DatasetId** column, locate the dataset GUID you noted in step 5. Multiple entries of the same GUID might display.

8.  Locate the aggregation type from the list in the **AggregationTypeId** column by using the following values:

    -   0 \= raw, nonaggregated data

    -   10 \= subhourly

    -   20 \= hourly

    -   30 \= daily

After you have located the dataset and its aggregation type, scroll to the **MaxDataAgeDays** column, and then edit the value there to set the grooming interval.

## See Also
[Maintenance of Operations Manager](./Maintenance-of-Operations-Manager.md)
[Monitoring the Health of the Management Group](./Monitoring-the-Health-of-the-Management-Group.md)
[Inventory of Operations Manager Infrastructure](./Inventory-of-Operations-Manager-Infrastructure.md)
[Scheduling Maintenance in Operations Manager](./Scheduling-Maintenance-in-Operations-Manager.md)
[How and When to Clear the Cache](./How-and-When-to-Clear-the-Cache.md)
[How to Restart a Management Server](./How-to-Restart-a-Management-Server.md)
[How to Configure Grooming Settings for the Operations Manager Database](./How-to-Configure-Grooming-Settings-for-the-Operations-Manager-Database.md)
[How to Configure Grooming Settings for .NET Application Performance Monitoring Events](http://go.microsoft.com/fwlink/?LinkId=255375)
[Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](./Recommendations-for-Daily,-Weekly,-and-Monthly-Operations-Manager-Tasks.md)


