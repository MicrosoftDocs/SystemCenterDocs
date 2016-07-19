---
title: How to Determine When Data Warehouse Registration Is Complete
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57af5610-04dd-40ca-87e4-545453d206ec


















---
# How to Determine When Data Warehouse Registration Is Complete
Several management packs are imported during the data warehouse registration process in System Center 2012 - Service Manager. Data warehouse registration is complete when all of the management packs have been imported. You will have to determine when that process is complete by using the following procedure.  
  
### To determine when management pack deployment has completed  
  
1.  Start the Service Manager console.  
  
2.  In the Service Manager console, select **Data Warehouse**.  
  
3.  In the **Data Warehouse** pane, expand **Data Warehouse**, and then click **Data Warehouse Jobs**.  
  
4.  In the **Data Warehouse Jobs** pane, click **MPSyncJob**.  
  
5.  In the **MPSyncJob** details pane, in the **Synchronization Job Details** list, scroll to the right to view the **Status** column, and then click **Status** to alphabetically sort the status column.  
  
6.  Scroll through the **Status** list. The management pack deployment process is complete when the status for all of the management packs is **Associated** or **Imported**. Make sure that there is no status of either **Pending Association** or **Failed** in the status list. In the **Data Warehouse Jobs** pane, the status of the **MPSyncJob** will have changed from **Running** to **Not Started** when the registration process is complete. This deployment process can take up to two hours to complete.  
  
7.  Use the following steps to periodically refresh the **Data Warehouse Job** pane to monitor the progress of the registration process:  
  
    1.  In the **Tasks** pane, under **Data Warehouse Jobs**, click **Refresh**.  
  
    2.  In the **Data Warehouse Jobs** pane, click **MPSyncJob**.  
  
    3.  In the **MPSyncJob** details pane, in the **Synchronization Job Details** list, scroll to the right to view the **Status** column, and then click **Status** to alphabetically sort the status column.  
  
8.  After the management packs have been deployed \(as determined in step 6\), make sure that the following five data warehouse jobs appear in the **Data Warehouse Jobs** pane:  
  
    -   Extract\_\<Service Manager management group name\>  
  
    -   Extract\_\<data warehouse management group name\>  
  
    -   Load.Common  
  
    -   Transform.Common  
  
    -   MPSyncJob  
  
    > [!NOTE]  
    >  If these five data warehouse jobs do not appear, complete the following steps:  
    >   
    >  1.  In the **Data Warehouse Jobs** pane, click **MPSyncJob**.  
    > 2.  In the **Tasks** pane, under **Synchronization**, click **Resume**.  
    > 3.  Determine whether management pack deployment is complete by repeating steps 4through 6.
