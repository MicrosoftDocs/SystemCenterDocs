---
ms.assetid: c4e4d992-340a-4ab9-8c98-6640c37adda2
title:  How to Suspend Monitoring Temporarily by Using Maintenance Mode
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---


# How to suspend monitoring temporarily by using maintenance mode

>Applies To: System Center 2016 - Operations Manager

Maintenance mode in Operations Manager enables you to avoid any alerts or errors that might occur when a monitored object, such as a computer, a SQL database, or distributed application, is taken offline for maintenance. Maintenance mode suspends the following features:

-   Rules and monitors

-   Notifications

-   Automatic responses

-   State changes

-   New alerts

For example, an Exchange mailbox role running on a Windows server will have an Exchange Server service pack applied. This software update maintenance is expected to take 60 minutes to complete. During this time, the Mailbox database running on this server will not be available.

In this case, we can put the Exchange Mailbox role and contained components into Maintenance Mode instead of putting the entire computer into Maintenance Mode. This way we can continue to monitor the other components running on the server, including the Windows operating system, while maintenance is performed specifically to the Exchange Server application.

You can either select one or more monitoring objects and place them into maintenance mode on-demand, or you can define schedules aligned with your service or maintenance windows, and automatically place them into maintenance mode in the future according to the schedule you choose.  With the new scheduling feature, you can:

- Schedule maintenance mode at a future time daily, weekly, or monthly.

- Choose different classes of entities and groups to put to maintenance as a part of a single schedule.

- View all the maintenance mode schedules from a single screen.

- Schedule multiple jobs for the same monitored entity.

> [!IMPORTANT]
> Important Information about configuring and working with the Maintenance Schedule feature:
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
>   For more information about setting the SDK action account see [Account Information for Operations Manager](../plan/planning-security-accounts.md#system-center-configuration-service- and-system-center-data-access-service-account)

To support the scenario of initiating maintenance mode directly from the agent-managed computer, Operations Manager now supports allowing a server administrator to set the machine in maintenance mode directly from the computer itself, without needing to perform this from the Operations console.  This can be performed with the new PowerShell cmdlet **Start-SCOMAgentMaintenanceMode**.  

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


### Enable from Target System

Maintenance mode can be enabled directly from the monitored Windows computer by a server administrator using the PowerShell cmdlet **Start-SCOMAgentMaintenanceMode**.  When server administrator or operator runs the PowerShell cmdlet on the computer, the command creates an entry in the registry which stores arguments for Maintenance Mode, such as duration, reason, comment and information like time of invocation of cmdlet. The comment field contains user information, specifically who has invoked maintenance mode. A rule that targets the agent, runs every 5 minutes to read this registry entry on the agent with a PowerShell script  **ReadMaintenanceModeRegEntry.ps1**, and then marks this entry as invalid so at next invocation it will not pick this entry. The write action, which is part of the rule and targets the management server, takes this record and sets maintenance mode for the agent based on the record read from the registry.  The frequency the rule runs can be overridden to a custom interval.  

**Start-SCOMAgentMaintenanceMode** has the following syntax:

    `Start-SCOMAgentMaintenanceMode -Duration <Double (in minutes)> [-Reason <string>] [-Comments <string>]`

> [!NOTE] 
> The minimum duration value accepted is five (5) minutes.


The following reasons are accepted by the cmdlet:  

- PlannedOther
- UnplannedOther
- PlannedHardwareMaintenance
- UnplannedHardwareMaintenance
- PlannedHardwareInstallation
- UnplannedHardwareInstallation
- PlannedOperatingSystemReconfiguration
- UnplannedOperatingSystemReconfiguration
- PlannedApplicationMaintenance
- UnplannedApplicationMaintenance
- ApplicationInstallation
- ApplicationUnresponsive
- ApplicationUnstable
- SecurityIssue
- LossOfNetworkConnectivity  

#### Examples:

1. To enable for an interval of five (5) minutes and with a major reason of **Planned** and minor reason **Other** type:

    `Start-SCOMAgentMaintenanceMode -Duration 5 –Reason PlannedOther` 

2. To enable for an interval of ten (10) minutes with no reason, type:

    `Start-SCOMAgentMaintenanceMode -Duration 10`

Perform the following steps to initiate maintenance mode from the target Windows computer.

1. Log onto the computer.

2. On computers running Windows Server 2012 and higher, to run Windows PowerShell as an administrator from the **Start** screen, right-click the **Windows PowerShell** tile, and in the app bar, click **Run as administrator**.  

3. Change directory to the following path **C:\Program Files\Microsoft Monitoring Agent\Agent** by typing `cd C:\Program Files\Microsoft Monitoring Agent\Agent`.

4. Import the module MaintenanceMode.dll by typing `Import-module MaintenanceMode.dll`.   

5. Type **Start-SCOMAgentMaintenanceMode** and use the parameters to configure the maintenance mode request. 

> [!NOTE]  
> To confirm that Maintenance Mode request is successful you can look in the Operations Manager Event Log for an Event ID 2222 followed by one or more events with Event ID 1215. If Event ID 2222 is present but ID 1215 is missing, this indicates the maintenance mode request was missed. You will need to re-raise the request.  

> In order to re-raise the request you will need to remove the record in the registry for maintenance mode using following command and then re-run the ***Start-SCOMAgentMaintenanceMode** cmdlet:
> `Set-ItemProperty -Path "HKLM:\software\Microsoft\Microsoft Operations Manager\3.0\MaintenanceMode" -Name record -Value "" `  


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

7. On the **Object Selection** page, click **Next**.

8. In the **Create Maintenance Schedule** wizard, on the **Schedule** page, you can specify the following for your maintenance schedule:

   - Choose the frequency as to how often you would like it to run.  If you select the option **Once**, the task will only run one time based on the start date and time selected.
   - Under **Duration** select the **Start Time** and for **End Time**, select the **number of minutes** or select and enter the **Specific end time**.  
   - Under **Schedule is effective beginning**, specify when this schedule is allowed to take effect and if you require it to no longer be valid after a period of time, click the option **The schedule expires on** and select a future expiration date.  

     > [!NOTE]
     > The minimum value for Number of minutes is 5. The maximum value is 1,051,200 (2 years). 
  
9. Click **Next** once you have completed configuring the schedule options.

10. In the **Create Maintenance Schedule** wizard, on the **Details** page, specify the following:

   - Create a name for the schedule in the **Schedule Name** box.
   - Select **Planned** if this is a planned event; otherwise, leave it cleared.
   - In the **Category** list, click the appropriate maintenance category.
   - Select **Enable Schedule** if you want to enable the schedule now, or clear it if you plan on enabling the schedule later.

11. Click **Finish** to save your changes.  

The new schedule will appear in the list of maintenance schedules and you can edit, disable, or delete a maintenance schedule from the list.  This can be accomplished by selecting the schedule from the list and choosing the corresponding option from the **Tasks** pane.    
