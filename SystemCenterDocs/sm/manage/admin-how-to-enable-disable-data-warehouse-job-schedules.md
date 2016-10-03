---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Enable or Disable Data Warehouse Job Schedules
ms.technology:  service-manager
ms.assetid:  f87dfbc3-d82b-428f-8dc4-e6a8129fd79f
---

# How to Enable or Disable Data Warehouse Job Schedules

>Applies To: System Center 2016 - Service Manager

# How to Enable Data Warehouse Job Schedules

Use the following procedure to enable the schedule for the ETL jobs as needed; you can use this procedure to enable the schedule for any of the data warehouse jobs. By default, the schedules for the extract, transform, and load (ETL) jobs are enabled. In this release of Service Manger, you can enable the schedules only by using Windows PowerShell.

### To enable a schedule for a data warehouse job by using a Windows PowerShell cmdlet

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and click **Service Manager Shell**.

2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Enable-SCDWJobSchedule -JobName Extract_<data warehouse management group name>
    ```

    ```
    Enable-SCDWJobSchedule -JobName Extract_<Service Manager management group name>
    ```

    ```
    Enable-SCDWJobSchedule -JobName Transform.Common
    ```

    ```
    Enable-SCDWJobSchedule -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.

## How to Disable a Data Warehouse Job Schedule

You can use the following procedure to disable the schedule for the extract, transform, and load (ETL) jobs; however, you can use this procedure to disable the schedule for any data warehouse job. In this release of Service Manager, you can disable the schedules only by using Windows PowerShell cmdlets.


### To disable a schedule for a data warehouse job by using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  At the Windows PowerShell prompt, type the following commands, and press ENTER after each command:

    ```
    Disable-SCDWJobSchedule -JobName Extract_<data warehouse management group name>
    ```

    ```
    Disable-SCDWJobSchedule -JobName Extract_<Service Manager management group name>
    ```

    ```
    Disable-SCDWJobSchedule -JobName Transform.Common
    ```

    ```
    Disable-SCDWJobSchedule -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.
