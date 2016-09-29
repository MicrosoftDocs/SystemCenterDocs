---
title: How to Register the Data Warehouse Server in the Lab Environment
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab0ec9ba-ba35-4a29-b933-472dfd18276a
---

# How to Register the Data Warehouse Server in the Lab Environment

>Applies To: System Center 2016 - Service Manager

Use the following procedure to register the newly installed data warehouse server with the lab Service Manager environment.  

### To register a data warehouse  

1.  Log on to the computer that hosts the Service Manager console. Use an account that is a member of the Service Manager and data warehouse management administrators group.  

2.  In the Service Manager console, click **Administration**.  

3.  In the **Administration** pane, expand **Administration**.  

4.  In the **Administration** view, in the **Register with Service Manager's Data Warehouse** area, click **Register with Service Manager Data Warehouse**.  

5.  In the Data Warehouse Registration wizard, on the **Before You Begin** page, click **Next**.  

6.  On the **Data Warehouse** page, in the **Server name** box, type the fully qualified domain name of the computer hosting the data warehouse management server, and then click **Test Connection**. If the test is successful, click **Next**.  

7.  On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your own choosing.  

    > [!IMPORTANT]  
    >  The account you specify will be assigned administrative credentials on the Service Manager management server and granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when registering with the data warehouse.  

8.  On the **Summary** page, click **Create**.  

9. On the **Completion** page, when **The data warehouse registration succeeded** is displayed, click **Close**.  

10. A dialog box states that the report deployment process has not finished. This is to be expected. On the **System Center Service Manager** dialog box, click **OK**.  

11. In a few minutes, after closing the Data Warehouse Registration wizard, the **Data Warehouse** button will be added to the Service Manager console. In the Service Manager console, click the arrow at the lower right corner of the Service Manager console buttons, and then click **Show More Buttons**.  

 You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to register Service Manager management groups with the data warehouse, see [Add\-SCDWMgmtGroup](http://go.microsoft.com/fwlink/p/?LinkId=203096).  

### To validate the data warehouse registration process  

1.  On the computer hosting the data warehouse management server, start Windows PowerShell with administrative credentials.  

2.  At the Windows PowerShell command prompt, type the following commands, and then press ENTER:  

    ```  
    Set-ExecutionPolicy RemoteSigned  
    Import-Module .\Microsoft.EnterpriseManagement.Warehouse.Cmdlets.psd1  

    ```  

3.  Type the following command, and then press ENTER.  

    ```  
    Get-SCDWMgmtGroup  

    ```  

4.  If registration was successful, a table with two rows of data is displayed. One row displays data for the data warehouse management group, and a second row displays data for the Service Manager management group. If registration fails, only the data for the data warehouse management group is displayed.  

## Determine when the deployment is complete  
 Because you need to allow enough time for the management pack deployment process to be completed, you will have to determine when that process is complete. You can use the following procedure in Service Manager to determine when the process is complete.  

#### To determine when management pack deployment has completed  

1.  Start the Service Manager console.  

2.  In the Service Manager console, click **Data Warehouse**.  

3.  In the **Data Warehouse** pane, expand **Data Warehouse**, and then click **Data Warehouse Jobs**.  

4.  In the **Data Warehouse Jobs** pane, click **MPSyncJob**.  

5.  In the **Tasks** pane, under **Synchronization**, click **Details**.  

6.  In the **MP Sync Job** dialog box, scroll to the right and examine the **Status** column.  

    > [!NOTE]  
    >  In the **MP Sync Job** dialog box, click **Status** to alphabetically sort the status column.  

7.  Scroll through the **Status** list. The management pack deployment process is complete when **Associated** or **Imported** is listed in the status column for all of the management packs. Make sure that there is no status of either **Pending Association** or **Failed** in the status list. In the **Data Warehouse Jobs** pane, the status of the **MPSyncJob** will have changed from **Running** to **Not Started**. This deployment process can take up to two hours to complete.  

8.  To refresh the **MP Sync Job** dialog box:  

    1.  Press **OK** to close the dialog box.  

    2.  In the **Tasks** pane, in the **Data Warehouse Jobs** area, click **Refresh**.  

    3.  In the **Data Warehouse Jobs** pane, click **MPSyncJobs**.  

    4.  In the **Tasks** pane, under **Synchronization**, click **Details**.  

9. After the management packs have been deployed \(as determined in step 7\), make sure that the following 5 data warehouse jobs are displayed in the **Data Warehouse Jobs** pane:  

    -   Extract\_\<Service Manager management group name\>  

    -   Extract\_\<data warehouse management group name\>  

    -   Load.Common  

    -   Transform.Common  

    -   MPSyncJob  

10. If these 5 data warehouse jobs are not displayed, perform the following procedure:  

    1.  In the **Data Warehouse Jobs** pane, click **MPSyncJob**.  

    2.  In the **Tasks** pane, under **Synchronization**, click **Resume**.  

    3.  Assess if management pack deployment has completed by returning to step 4 above.
