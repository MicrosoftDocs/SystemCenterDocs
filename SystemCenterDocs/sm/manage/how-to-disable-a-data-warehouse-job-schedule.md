---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Disable a Data Warehouse Job Schedule
ms.technology:  service-manager
ms.assetid:  fff90c14-a2bd-4f92-95a5-b708203d2f06
---

# How to Disable a Data Warehouse Job Schedule

>Applies To: System Center 2016 Technical Preview - Service Manager

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
