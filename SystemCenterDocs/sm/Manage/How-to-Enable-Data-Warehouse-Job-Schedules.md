---
title: How to Enable Data Warehouse Job Schedules
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f87dfbc3-d82b-428f-8dc4-e6a8129fd79f
---
# How to Enable Data Warehouse Job Schedules

>Applies To: System Center 2016 Technical Preview - Service Manager

Use the following procedure to enable the schedule for the ETL jobs as needed; you can use this procedure to enable the schedule for any of the data warehouse jobs. By default, the schedules for the extract, transform, and load (ETL) jobs are enabled. In this release of Service Manger, you can enable the schedules only by using Windows PowerShell.

### To enable a schedule for a data warehouse job by using a Windows PowerShell cmdlet

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and click **Service Manager Shell**.

2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Enable-SCDWJobSchedule –JobName Extract_<data warehouse management group name>
    ```

    ```
    Enable-SCDWJobSchedule –JobName Extract_<Service Manager management group name>
    ```

    ```
    Enable-SCDWJobSchedule –JobName Transform.Common
    ```

    ```
    Enable-SCDWJobSchedule –JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.



