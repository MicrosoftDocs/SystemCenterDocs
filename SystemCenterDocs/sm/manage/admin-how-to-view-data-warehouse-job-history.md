---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to View Data Warehouse Job History
ms.technology:  service-manager
ms.assetid:  a389dcf8-28f3-4f0e-a67b-d8f9f3f93a41
---

# How to View Data Warehouse Job History

>Applies To: System Center 2016 - Service Manager

A history of data warehouse jobs is collected as they run in Service Manager. You can view this history to determine how long a job ran or to determine the last time the job ran successfully. When you display the data warehouse job history, you display the number of entries that you specify by using the *NumberOfBatches* parameter. Use the following procedure to view the last five entries in the history of a data warehouse job.

### To view the last five entries in the data warehouse job history

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  Type the following command, and then press ENTER.

    ```
    Get-SCDWJob -NumberOfBatches 5
    ```

3.  Type **exit**, and then press ENTER.



