---
title: Scheduling Maintenance in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78329674-d244-44cb-b03e-6dc3b6362468
---
# Scheduling Maintenance in Operations Manager
This topic details the default schedule for [!INCLUDE[om12long](../Token/om12long_md.md)] maintenance tasks.

## Maintenance Tasks Schedule
By default, [!INCLUDE[om12short](../Token/om12short_md.md)] performs maintenance tasks daily to maintain optimal performance of the Operations Manager database.  These maintenance tasks are defined as system rules in the Operations Manager management pack.

The following table displays the maintenance tasks and the time they are scheduled to run:

|Task|Description|Schedule|
|--------|---------------|------------|
|Discovery Data Grooming|A rule that deletes aged discovery data from the Operations Manager database.|Every day at 2 AM|
|Partition and Grooming|A rule that runs workflows to partition and deletes aged data from the Operations Manager database.|Every day at 12 AM|
|Detect and Fix Object Space Inconsistencies|A rule that repairs data block corruption in database schema objects.|Every 30 minutes|
|Alert Auto Resolve Execute All|A rule that automatically resolves active alerts after a period of time.|Every day at 4 AM|

#### To check the schedules for the grooming jobs

1.  In the Operations console, click **Authoring**.

2.  Under **Authoring**, expand **Management Pack Objects**, and then click **Rules**.

3.  In the **Rules** pane, change the scope of management pack objects by clicking **Scope**.

4.  In the **Scope Management Pack Objects by target\(s\)** dialog box, click **Clear All**.

5.  In **Look for**, type **All Management Servers Resource Pool** to locate the target from the System Center Core Library.

6.  Select **All Management Servers Resource Pool**, and then click **OK**.

7.  In the **Rules** pane, right\-click the specific rule, and then click **Properties**.

8.  In the **Properties** dialog box, click the **Configuration** tab.

9. Under **Data Sources**, click **View** to display the configured schedule for the rule.

10. Click **Close** twice to close the **Properties** dialog box.

    > [!NOTE]
    > The scheduled times of the grooming jobs cannot be reconfigured by using an override. If you need to change the schedules of these maintenance tasks, you must first disable them with an override and then create new system rules that match the configuration of the original rules with new schedules.

## See Also
[Maintenance of Operations Manager](../Topic/Maintenance-of-Operations-Manager.md)
[Monitoring the Health of the Management Group](../Topic/Monitoring-the-Health-of-the-Management-Group.md)
[Inventory of Operations Manager Infrastructure](../Topic/Inventory-of-Operations-Manager-Infrastructure.md)
[How to Configure Grooming Settings for the Reporting Data Warehouse Database](../Topic/How-to-Configure-Grooming-Settings-for-the-Reporting-Data-Warehouse-Database.md)
[How and When to Clear the Cache](../Topic/How-and-When-to-Clear-the-Cache.md)
[How to Restart a Management Server](../Topic/How-to-Restart-a-Management-Server.md)
[How to Configure Grooming Settings for the Operations Manager Database](../Topic/How-to-Configure-Grooming-Settings-for-the-Operations-Manager-Database.md)
[Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](../Topic/Recommendations-for-Daily,-Weekly,-and-Monthly-Operations-Manager-Tasks.md)

