---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Stop and Start a Data Warehouse Job
ms.technology:  service-manager
ms.assetid:  ab2b063e-6094-4ec5-9ecc-48754c30438c
---

# How to Stop and Start a Data Warehouse Job

>Applies To: System Center 2016 Technical Preview - Service Manager

You can stop and start data warehouse jobs that are running in Service Manager. For example, you might have to stop all of the data warehouse jobs that are running to ensure that a security update to the data warehouse management server does not interfere with any jobs that might run. After the server has been updated and restarted, you resume all the data warehouse jobs. You can stop and then start jobs by using the Service Manager console or by using Windows PowerShell cmdlets. In this example, only the extract, transform, and load (ETL) jobs are running.

> [!NOTE]
> For information about using the Service Manager Windows PowerShell cmdlets, see [Getting Started with Service Manager Cmdlets for Windows PowerShell](Getting-Started-with-Service-Manager-Cmdlets-for-Windows-PowerShell.md).

### To stop and start data warehouse jobs using the Service Manager console

1.  In the Service Manager console, click **Data Warehouse**.

2.  Expand **Data Warehouse**, and then click **Data Warehouse Jobs**.

3.  In the **Data Warehouse Jobs** pane, select a job that is running, and then click **Suspend** in the **Tasks** list.

4.  Repeat the previous step for each data warehouse job.

5.  To resume each job, select a job that is stopped in the **Data Warehouse Jobs** pane, and then click **Resume** in the **Tasks** list.

### To stop all data warehouse jobs using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Stop-SCDWJob-JobName Extract_<data warehouse management group name>
    ```

    ```
    Stop-SCDWJob -JobName Extract_<Service Manager management group name>
    ```

    ```
    Stop-SCDWJob -JobName Transform.Common
    ```

    ```
    Stop-SCDWJob -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.

### To start all data warehouse jobs using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  At the Windows PowerShell prompt, type the following commands, and then press ENTER after each command:

    ```
    Start-SCDWJob -JobName Extract_<data warehouse management group name>
    ```

    ```
    Start-SCDWJob -JobName Extract_<Service Manager management group name>
    ```

    ```
    Start-SCDWJob -JobName Transform.Common
    ```

    ```
    Start-SCDWJob -JobName Load.Common
    ```

3.  Type **exit**, and then press ENTER.
