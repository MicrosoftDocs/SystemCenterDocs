---
title: Enable Service Manager Reporting
description: Use the Data Warehouse Registration wizard to enable reporting.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 03/31/2025
ms.update-cycle: 1095-days
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: d5795bd5-7c01-47b9-909f-8147362b9cf4
---

# Register with the Service Manager data warehouse to enable reporting



After you've deployed the Service Manager management servers and data warehouse management servers, for reporting to function you must run the Data Warehouse Registration Wizard. This wizard registers the Service Manager management group with the data warehouse management group. It also deploys management packs from the Service Manager management server to the data warehouse management server.  

 The management pack deployment process can take several hours to complete. It's a best practice not to turn off any Service Manager computers or stop any Service Manager services during this time. During this registration process, you can continue to use the Service Manager console to perform any Service Manager functions that you want.  

 To ensure that reporting data will be available, use the procedures in the following sections to register the data warehouse and deploy the management packs.  

## Run the Data Warehouse Registration wizard

To use the Data Warehouse Registration Wizard to register with the Service Manager data warehouse, in System Center - Service Manager, follow these steps:

1. By using an account that is a member of the Service Manager and data warehouse management administrators group, sign in to the computer that hosts the Service Manager console.  

2. In the Service Manager console, select **Administration**.  

3. In the **Administration** pane, expand **Administration**.  

4. In the **Administration** view, in the **Register with Service Manager's Data Warehouse** area, select **Register with Service Manager Data Warehouse**.  

5. In the Data Warehouse Registration wizard, on the **Before You Begin** page, select **Next**.  

6. On the **Data Warehouse** page, in the **Server name** box, enter the *fully qualified domain name* \(FQDN\) of the computer hosting the data warehouse management server, and select **Test Connection**. If the test is successful, select **Next**.  

7. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and select **Next**, or you can enter credentials from a user or group of your own choosing.  

   > [!IMPORTANT]  
   > The account that you specify will be assigned administrative credentials on the Service Manager management server, and it will be granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when you're registering with the data warehouse.  

8. On the **Summary** page, select **Create**.  

9. On the **Completion** page, when **The data warehouse registration succeeded** appears, select **Close**.  

10. A dialog states that the report deployment process isn't finished. This is to be expected. On the **System Center Service Manager** dialog, select **OK**.  

11. In a few minutes, after you close the Data Warehouse Registration Wizard, the **Data Warehouse** button will be added to the Service Manager console. In the Service Manager console, select the arrow at the lower right corner of the Service Manager console buttons, and select **Show More Buttons**.  

    ![Screenshot of Windows PowerShell.](./media/register-dw/pssymbol.png) You can use a Windows&nbsp;PowerShell command to complete this task. For information about how to use Windows&nbsp;PowerShell to register Service Manager management groups with the data warehouse, see [Add\-SCDWMgmtGroup](/previous-versions/system-center/service-manager-2010-sp1/ff951619(v=technet.10)).

## Determine when Data Warehouse registration is complete

Several management packs are imported during the data warehouse registration process in Service Manager. Data warehouse registration is complete when all of the management packs have been imported. You'll have to determine when that process is complete by using the following procedure.  

To determine when management pack deployment has completed, follow these steps:

1. Start the Service Manager console.  

2. In the Service Manager console, select **Data Warehouse**.  

3. In the **Data Warehouse** pane, expand **Data Warehouse**, and select **Data Warehouse Jobs**.  

4. In the **Data Warehouse Jobs** pane, select **MPSyncJob**.  

5. In the **MPSyncJob** details pane, in the **Synchronization Job Details** list, scroll to the right to view the **Status** column, and select **Status** to alphabetically sort the status column.  

6. Scroll through the **Status** list. The management pack deployment process is complete when the status for all of the management packs is **Associated** or **Imported**. Ensure that there's no status of either **Pending Association** or **Failed** in the status list. In the **Data Warehouse Jobs** pane, the status of the **MPSyncJob** will have changed from **Running** to **Not Started** when the registration process is complete. This deployment process can take up to two hours to complete.  

7. To periodically refresh the **Data Warehouse Job** pane to monitor the progress of the registration process, do the following:

   1. In the **Tasks** pane, under **Data Warehouse Jobs**, select **Refresh**.  

   2. In the **Data Warehouse Jobs** pane, select **MPSyncJob**.  

   3. In the **MPSyncJob** details pane, in the **Synchronization Job Details** list, scroll to the right to view the **Status** column, and then select **Status** to alphabetically sort the status column.  

8. After the management packs have been deployed \(as determined in step 6\), ensure that the following five data warehouse jobs appear in the **Data Warehouse Jobs** pane:  

   - Extract\_\<Service Manager management group name\>  

   - Extract\_\<data warehouse management group name\>  

   - Load.Common  

   - Transform.Common  

   - MPSyncJob  

   > [!NOTE]
   > If these five data warehouse jobs don't appear, complete the following steps:  
   >
   > a. In the **Data Warehouse Jobs** pane, select **MPSyncJob**.  
   > b. In the **Tasks** pane, under **Synchronization**, and select **Resume**.  
   > c. Determine whether management pack deployment is complete by repeating steps 4 through 6.

## Next steps

- To install additional Service Manager management servers to improve performance, review [Deploy additional Service Manager management servers](deploy-additional-ms.md).
