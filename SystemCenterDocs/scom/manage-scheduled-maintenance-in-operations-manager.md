---
title: Scheduled Maintenance in Operations Manager
description: This article describes the default scheduled maintenance tasks configured automatically when the management group is installed.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: 78329674-d244-44cb-b03e-6dc3b6362468
---

# Scheduled Maintenance in Operations Manager



This topic details the default schedule for System Center Operations Manager maintenance tasks.  

## Maintenance Tasks Schedule  
By default, System Center Operations Manager performs maintenance tasks daily to maintain optimal performance of the Operations Manager database and data warehouse database.  These maintenance tasks are defined as system rules in the Operations Manager management pack.  

The following table displays the maintenance tasks and the time they're scheduled to run:  

|Task|Description|Schedule|  
|--------|---------------|------------|  
|Discovery Data Grooming|A rule that deletes aged discovery data from the Operations Manager database.|Every day at 2 AM|  
|Optimize Indexes|A rule that executes a daily database maintenance  stored procedure name *p_OptimizeIndexes* against some of the tables.  **This rule cannot be changed or modified.**|Every day at 2:30 AM|  
|Partition and Grooming|A rule that runs workflows to partition and deletes aged data from the Operations Manager database.|Every day at 12 AM|  
|Detect and Fix Object Space Inconsistencies|A rule that repairs data block corruption in database schema objects.|Every 30 minutes|  
|Alert Auto Resolve Execute All|A rule that automatically resolves active alerts after a period of time.|Every day at 4 AM|  
|Standard Data Warehouse Data Set maintenance rule|A rule that calls many other stored procedures to aggregate, optimize, and groom data in the data warehouse database.|Every 60 seconds|

### To check the schedules for the grooming jobs

1.  Log on to the computer with an account that is a member of the Operations Manager Administrator role.  

2.  Open the Operations console and in the console, click **Authoring** from the left-hand pane.  

2.  Under **Authoring**, expand **Management Pack Objects**, and then click **Rules**.  

3.  In the **Rules** pane, change the scope of management pack objects by clicking **Scope**.  

4.  In the **Scope Management Pack Objects by target(s)** dialog box, click **Clear All**.  

5.  In **Look for**, type **All Management Servers Resource Pool** to locate the target from the System Center Core Library.  

6.  Select **All Management Servers Resource Pool**.

7.  In **Look for**, type **Standard Data Set** to locate the target and select it.  Click **OK**.

8.  In the **Rules** pane, right-click the specific rule listed in the table earlier, and then click **Properties**.  

9.  In the **Properties** dialog box, click the **Configuration** tab.  

10. Under **Data Sources**, click **View** to display the configured schedule for the rule.  

11. Click **Close** twice to close the **Properties** dialog box.  

    > [!NOTE]  
    > The scheduled times of the grooming jobs cannot be reconfigured by using an override. If you need to change the schedules of these maintenance tasks, you must first disable them with an override and then create new system rules that match the configuration of the original rules with new schedules.  

## Next steps

- To learn more about the default retention period for the different data types stored in the Operations Manager Reporting data warehouse database and how to modify those settings, please see [How to configure grooming settings for the Operations Manager Reporting data warehouse database](manage-omdwdb-grooming-settings.md).

- To learn more about the default retention period for the different data types stored in the Operations Manager operational database and how to modify those settings, please see
[How to configure grooming settings for the Operations Manager database](manage-omdb-grooming-settings.md).

- See also [Monitoring the Health of the Management Group](manage-monitor-health-mg.md) to understand how you can quickly assess the functional state of your management group.  
