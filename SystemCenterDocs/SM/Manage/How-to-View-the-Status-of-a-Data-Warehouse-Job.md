---
title: How to View the Status of a Data Warehouse Job
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80fa4de-39bc-4463-bb29-661575b0b1ab
---
# How to View the Status of a Data Warehouse Job
You can use the following procedures to view the status of a data warehouse job in Service Manager to determine whether a job is running, stopped, or failed.


### To view the status of a data warehouse job by using the [!INCLUDE[smcons](../../Token/smcons_md.md)]

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Data Warehouse**.

2.  In the **Data Warehouse** pane, expand **Data Warehouse**, and then click **Data Warehouse Jobs**.

3.  In the **Data Warehouse Jobs** pane, review the list of jobs to view their status.

### To view the status of a data warehouse job by using a Windows PowerShell cmdlet

1.  On the computer that hosts the data warehouse management server, click **Start**, point to **All Programs**, click **Microsoft System Center**, click **Service Manager 2016**, and then click **Service Manager Shell**.

2.  Type the following command, and then press ENTER.

    ```
    Get-SCDWJob
    ```

3.  Review the list of jobs to view their status.


