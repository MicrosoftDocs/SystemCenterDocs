---
title: How to Manage Data Import Jobs for Operations Manager and Configuration Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24cdcc7c-8b46-42a0-a699-d5061b01aec6
---
# How to Manage Data Import Jobs for Operations Manager and Configuration Manager
You can use the following procedure to manage data warehouse data import jobs in Service Manager. Data import jobs are like other data warehouse jobs, and you can manage them with the [!INCLUDE[smcons](../Token/smcons_md.md)] and also with Windows PowerShell cmdlets. Methods of management include:

-   Revising the processing schedule to hourly, daily, or weekly

-   Suspending a job

-   Resuming a suspended, or Not Started, job

### To manage data import jobs and change a job schedule

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Data Warehouse**, expand **Data Warehouse**, and then click **Data Warehouse Jobs**.

2.  In the **Data Warehouse Jobs** pane, select a job name, and then under **Tasks**, click **Properties**.

3.  In the job properties dialog box that appears, you can view the current schedule. You can change the schedule to one of your choice. For example, change the schedule to **Daily** and run the job at **1:00 AM**, and then click **OK**.

4.  You can optionally **Suspend** jobs, and you can **Resume** any that are suspended or Not Started.

