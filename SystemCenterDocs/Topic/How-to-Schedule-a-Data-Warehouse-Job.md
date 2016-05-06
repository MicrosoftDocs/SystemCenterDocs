---
title: How to Schedule a Data Warehouse Job
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f33a637-c203-4146-b1ae-5fb63b349b94
---
# How to Schedule a Data Warehouse Job
You can use the following procedure to schedule a data warehouse job in Service Manager.

You could use this procedure in a scenario where a schedule for the data warehouse jobs has been defined in [!INCLUDE[smshort](../Token/smshort_md.md)]. You want to change the schedule for the data warehouse jobs to define standard maintenance windows for the [!INCLUDE[smshort](../Token/smshort_md.md)] database and for the data warehouse. Use the **Set\-SCDWJobSchedule** cmdlet to schedule the data warehouse jobs. The **Set\-SCDWJobSchedule –ScheduleType Weekly** cmdlet and parameter combination allows jobs to run only on the days you specify. For example, the following commands define a daily or weekly schedule:

```
Set-SCDWJobSchedule -JobName Transform.Common –ScheduleType Daily -DailyFrequency  01:00:00 -DailyStart 06:00

```

```
Set-SCDWJobSchedule -JobName Transform.Common -ScheduleType Weekly -WeeklyFrequency Tuesday, Thursday -WeeklyStart 06:00
```

> [!NOTE]
> To run Windows PowerShell cmdlets, the execution policy must be set to RemoteSigned.

In the following procedure, you configure a schedule for the Transform job to run every 45 minutes, starting at 2:00 in the morning. However, you can modify the commands to set your own schedule.

### To configure a schedule for data warehouse jobs

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  At the Windows PowerShell prompt, type the following command, and then press ENTER.

    ```
    Set-SCDWJobSchedule -JobName Transform.Common -ScheduleType Daily –DailyFrequency 00:45:00 –DailyStart 02:00
    ```

### To validate a data warehouse job schedule

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  Type the following command, and then press ENTER:

    ```
    Get-SCDWJobSchedule
    ```

