---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  mgoedtel
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  How to Suspend Monitoring Temporarily by Using Maintenance Mode
ms.technology:  operations-manager
ms.assetid:  e929ecc9-ad1f-46f6-bb93-9e0aa02580b2
---



# How to Suspend Monitoring Temporarily by Using Maintenance Mode
Maintenance mode in Operations Manager enables you to avoid any alerts or errors that might occur when a monitored object, such as a computer, a SQL database, or distributed application, is taken offline for maintenance. Maintenance mode suspends the following features:

-   Rules and monitors

-   Notifications

-   Automatic responses

-   State changes

-   New alerts

For example, an Exchange mailbox role running on a Windows server will have an Exchange Server service pack applied. This software update maintenance is expected to take 60 minutes to complete. During this time, the Mailbox database running on this server will not be available. 

In this case, we can put the Exchange Mailbox role and contained components into Maintenance Mode instead of putting the entire computer into Maintenance Mode. This way we can continue to monitor the other components running on the server, including the Windows operating system, while maintenance is performed specifically to the Exchange Server application.

You can either select one or more monitoring objects and place them into maintenance mode on-demand , or you can define schedules aligned with your service or maintenance windows, and automatically place them into maintenance mode in the future according to the schedule you choose.  With the new scheduling feature, you can:

- Schedule maintenance mode at a future time daily, weekly, or monthly.

- Choose different classes of entities and groups to put to maintenance as a part of a single schedule.

- View all the maintenance mode schedules from a single screen.

- Schedule multiple jobs for the same monitored entity.

 >[!IMPORTANT] Important Information about configuring and working with the Maintenance Schedule feature:
> - You can change when a running schedule will end, but the change will only apply to the schedule that is running. If you want to edit the end time for future runs of that schedule, you must first stop the schedule and then apply your changes.
>
> - The time zone specified for the Windows computer hosting the Management Server role will be applied to the maintenance schedule.
>
> - Changes to accommodate daylight savings time are not automatically applied to maintenance schedules. You must manually edit the schedule to adjust for daylight savings time.
> 
> - You can get historical data for when a monitored entity went into maintenance mode by querying the MaintenanceModeHistory table in the Operations Manager database.
> 
> - The System Center Operations Manager SDK account must be a member of one of the following SQL Server roles in order to take advantage of the Maintenance Mode feature: 
>
>   - SQLAgentUserRole
>   - SQLAgentReaderRole
>   - SQLAgentOperatorRole
>
>   For more information about setting the SDK action account see [Account Information for Operations Manager](https://technet.microsoft.com/library/hh457003.aspx)

For example, an Exchange mailbox role running on a Windows server will have an Exchange Server service pack applied. This software update maintenance is expected to take 60 minutes to complete. During this time, the Mailbox database running on this server will not be available. 

In this case, we can put the Exchange Mailbox role and contained components into Maintenance Mode instead of putting the entire computer into Maintenance Mode. This way we can continue to monitor the other components running on the server, including the Windows operating system, while maintenance is performed specifically to the Exchange Server application.  

The following section describes how to work with the different options for the on-demand maintenance mode feature.

## On-Demand Maintenance Mode

### To put a monitored object into maintenance mode

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Monitoring**.

3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.

4.  In the **Windows Computers** pane, right-click the computer that you want to place into maintenance mode, click **Maintenance Mode**, and then click **Start Maintenance Mode**. You can use ctrl+click or shift+click to select multiple computers to place into maintenance mode.

5.  In the **Maintenance Mode Settings** dialog box, under **Apply to**, click **Selected objects only** if only the computer is to be placed into maintenance mode; otherwise, click **Selected objects and all their contained objects**.

6.  Select **Planned** if this is a planned event; otherwise, leave it cleared.

7.  In the **Category** list, click the appropriate maintenance category.

8.  Under **Duration**, select and enter the **Number of minutes** or select and enter the **Specific end time**, and then click **OK**. A maintenance mode icon appears in the **Computers** pane, in the **Maintenance Mode** column for the computer you selected.

    > [!NOTE]
    > The minimum value for **Number of minutes** is 5. The maximum value is 1,051,200 (2 years).

### To edit maintenance mode settings for a monitored object

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Monitoring**.

3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.

4.  Right-click the computer in the **Windows Computers** pane whose settings you want to edit, click **Maintenance Mode**, and then click **Edit Maintenance Mode settings**.

5.  In the **Maintenance Mode Settings** dialog box, edit the settings you want to change, and then click **OK**.

### To stop maintenance mode on a monitored object

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Monitoring**.

3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.

4.  In the **Windows Computers** pane, right-click the computer that you want to take out of maintenance mode, click **Maintenance Mode**, and then click **Stop Maintenance Mode**.

5.  In the **Maintenance Mode** dialog box, do the following:

    -   If you selected **Selected objects and all their contained objects** when you placed the computer into maintenance mode, select **Remove contained objects** and then click **Yes**.

    -   If you selected **Selected objects only**, clear **Remove contained objects** and then click **Yes**.

6.  In the **Windows Computers** pane, the maintenance mode icon disappears from the **Maintenance Mode** column for the computer you selected.

    > [!NOTE]
    > Because Operations Manager polls maintenance mode settings only once every 5 minutes, there can be a delay in an object's scheduled removal from maintenance mode.

## Scheduling Maintenance Mode
 
The following section describes how to work with the different options available for the maintenance mode scheduling feature.

### Create Maintenance Schedule
The following procedures describes how to create a maintenance schedule for selected monitored objects for a future date.  
  
1. Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. In the **Administration** workspace, expand **Device Management**, and then click **Maintenance Schedules**.
 
 4. From the **Tasks** pane click **Create Maintenance Schedule**.
 
 5. In the **Create Maintenance Schedule** wizard, on the **Object Selection** page, click **Add/Remove objects...** and the **Create Group Wizard - Object Selection** dialog box appears.

6. In the **Create Group Wizard - Object Selection** dialog box, perform the following:
   - In the **Search for list**, the default item **Computer** is selected. Alternatively, you can select **Computer Group** or a specific class such as **SQL Server 2012 DB Engine** from the drop-down list.     
   - Optionally, in the **Filter by part of the name** box, type all or part of the object name, and then click **Search**.
  - In the **Available items** box, select the desired objects, click **Add**, and then click **OK**.

6. On the **Object Selection** page,click **Next**.

7. In the **Create Maintenance Schedule** wizard, on the **Schedule** page, you can specify the following for your maintenance schedule:

   - Choose the frequency as to how often you would like it to run.  If you select the option **Once**, the task will only run one time based on the start date and time selected.
   - Under **Duration** select the **Start Time** and for **End Time**, select the **number of minutes** or select and enter the **Specific end time**.  
   - Under **Schedule is effective beginning**, specify when this schedule is allowed to take effect and if you require it to no longer be valid after a period of time, click the option **The schedule expires on** and select a future expiration date.  

     >[!NOTE] The minimum value for Number of minutes is 5. The maximum value is 1,051,200 (2 years).   
8. Click **Next** once you have completed configuring the schedule options.
          
9. In the **Create Maintenance Schedule** wizard, on the **Details** page, specify the following:

   - Create a name for the schedule in the **Schedule Name** box.
   - Select **Planned** if this is a planned event; otherwise, leave it cleared.
   - In the **Category** list, click the appropriate maintenance category.
   - Select **Enable Schedule** if you want to enable the schedule now, or clear it if you plan on enabling the schedule later.
 
10. Click **Finish** to save your changes.  

The new schedule will appear in the list of maintenance schedules and you can edit, disable, or delete a maintenance schedule from the list.  This can be accomplished by selecting the schedule from the list and choosing the corresponding option from the **Tasks** pane.    
         

