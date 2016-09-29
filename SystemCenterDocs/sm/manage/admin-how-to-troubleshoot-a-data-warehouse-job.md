---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Troubleshoot a Data Warehouse Job
ms.technology:  service-manager
ms.assetid:  53e50bfa-c0b9-4fdd-8d96-dd4aea852eb8
---

# How to Troubleshoot a Data Warehouse Job

>Applies To: System Center 2016 - Service Manager

In Service Manager, you may encounter problems related to data warehouse jobs. After the Data Warehouse Registration Wizard completes and after Reporting becomes available in the Service Manager console, you can start running reports. If, for example, the incident management report you run doesn't show updated data, you can use Windows PowerShell cmdlets to troubleshoot the problem.

You can use the first procedure to determine whether a job failed using Windows PowerShell cmdlets, and you can evaluate any error messages that this job created.

The second procedure can be used to change the default transform job timeout period. If you see that the data warehouse transform job does not complete successfully, then this may be due to the default 3-hour timeout period for the job being surpassed. This can happen due to the fact that a large volume of data is transformed in the data warehouse. To confirm that this is actually happening, you can view the Event Viewer in the Data Warehouse where messages similar to:  **Timeout expired. The timeout period elapsed prior to completion of the operation or the server is not responding.** can be seen for a module. As an example, you might see the message above for the TransformEntityRelatesToEntityFact module. To resolve the problem in this case, you can set the timeout period to be longer than the default value of 10800 seconds.

### To troubleshoot data warehouse jobs by using Windows PowerShell cmdlets

1.  On the computer that hosts the data warehouse management server, start **Windows PowerShell**.

2.  Type the following command, and then press ENTER.

    ```
    Get-SCDWJob
    ```

3.  Review the output, and locate any job with **Failed** status.

4.  Type the following command, and then press ENTER. In the command, specify the data warehouse job that failed as the value of the *JobName* parameter.

    ```
    Get-SCDWJobModule -JobName Transform.Common
    ```

5.  In the output, locate a status of "Failed," and then review the **Error Message** column for more information about why the data warehouse job failed.

6.  When you are ready to retry the failed job, in the Service Manager console, click **Data Warehouse**.

7.  Expand **Data Warehouse**, and then click **Data Warehouse Jobs**.

8.  In the **Data Warehouse Jobs** pane, select the failed job in the list, and then click **Resume** in the **Tasks** list.

### To override the default timeout period

1.  Edit the registry on the data warehouse management server and ensure that the key name **SqlCommandTimeout** under **SOFTWARE\Microsoft\System Center\2016\Common\DAL** exists and is of type DWORD. If it does not exist create it.

2.  Edit the value, which is in seconds, with a positive value.

3.  Restart the Microsoft Monitoring Agent service.

4.  You can resume the Transform.common job to see the change.
