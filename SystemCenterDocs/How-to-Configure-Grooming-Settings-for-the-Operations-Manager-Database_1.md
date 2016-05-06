---
title: How to Configure Grooming Settings for the Operations Manager Database_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca275bd1-7f72-410d-b018-3b7346cb30a8
---
# How to Configure Grooming Settings for the Operations Manager Database_1
The grooming process removes unnecessary data from the Operations Manager database in order to maintain performance by managing its size. It deletes unnecessary records. You can configure the grooming setting for the following record types:

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

Use the following procedure to specify when specific record types are deleted or groomed from the Operations Manager database of an Operations Manager management group. The default grooming setting for all record types is data older than 7 days.

### To configure database grooming settings for a management group

1.  In the Operations console, click **Administration**.

2.  In the navigation pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, right\-click **Database Grooming**, and then click **Properties**.

4.  In the **Global Management Group Settings \- Database Grooming** dialog box, select a record type, and then click **Edit**.

5.  In the dialog box for the record type, specify **Older than** days, and then click **OK**.

6.  In the **Global Management Group Settings \- Database Grooming** dialog box, select another record type to **Edit** or click **OK**.

## See Also
[Maintenance of Operations Manager](./Maintenance-of-Operations-Manager.md)
[Monitoring the Health of the Management Group](./Monitoring-the-Health-of-the-Management-Group.md)
[Inventory of Operations Manager Infrastructure](./Inventory-of-Operations-Manager-Infrastructure.md)
[Scheduling Maintenance in Operations Manager](./Scheduling-Maintenance-in-Operations-Manager.md)
[How and When to Clear the Cache](./How-and-When-to-Clear-the-Cache.md)
[How to Restart a Management Server](./How-to-Restart-a-Management-Server.md)
[How to Configure Grooming Settings for the Reporting Data Warehouse Database](./How-to-Configure-Grooming-Settings-for-the-Reporting-Data-Warehouse-Database.md)
[How to Configure Grooming Settings for .NET Application Performance Monitoring Events](http://go.microsoft.com/fwlink/?LinkId=255375)
[Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](./Recommendations-for-Daily,-Weekly,-and-Monthly-Operations-Manager-Tasks.md)


