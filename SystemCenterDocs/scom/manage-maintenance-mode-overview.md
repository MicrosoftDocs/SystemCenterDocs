---
ms.assetid: c4e4d992-340a-4ab9-8c98-6640c37adda2
title: Suspend Monitoring Temporarily by Using Maintenance Mode
description: This article describes how to put a monitored object into maintenance mode on-demand or using a schedule.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 02/04/2026
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.update-cycle: 365-days
---

# Suspend monitoring temporarily by using maintenance mode

Maintenance mode in Operations Manager enables you to avoid any alerts or errors that might occur when a monitored object, such as a computer, a SQL database, or distributed application, is taken offline for maintenance. Maintenance mode suspends the following features:

- Rules and monitors

- Notifications

- Automatic responses

- State changes

- New alerts

For example, an Exchange mailbox role running on a Windows server will have an Exchange Server service pack applied. This software update maintenance is expected to take 60 minutes to complete. During this time, the Mailbox database running on this server won't be available.

In this case, you can put the Exchange Mailbox role and contained components into Maintenance Mode instead of putting the entire computer into Maintenance Mode. This way you can continue to monitor the other components running on the server, including the Windows operating system, while maintenance is performed specifically to the Exchange Server application.

You can either select one or more monitoring objects and place them into maintenance mode on-demand, or you can define schedules aligned with your service or maintenance windows, and automatically place them into maintenance mode in the future according to the schedule you choose. With the new scheduling feature, you can:

- Schedule maintenance mode at a future time daily, weekly, or monthly.

- Choose different classes of entities and groups to put to maintenance as a part of a single schedule.

- View all the maintenance mode schedules from a single screen.

- Schedule multiple jobs for the same monitored entity.

> [!IMPORTANT]
> See the following important Information about configuring and working with the Maintenance Schedule feature:
> - You can change when a running schedule will end, but the change will only apply to the schedule that's running. If you want to edit the end time for future runs of that schedule, you must first stop the schedule and then apply your changes.
>
> - With Operations Manager 2019 UR2, the furthest time is taken when a maintenance schedule is changed. See [detailed example](#furthest-end-time-during-schedule-overlap).
>
> - While creating or editing a maintenance schedule, you can't include more than 216 Objects at a time. If the number of objects exceeds 216, the following error message appears:
>  **The client has been disconnected from the server. Please call ManagementGroup.Reconnect() to reestablish the connection.**
>
>   To include more than 216 objects, create a single or multiple [groups](manage-create-manage-groups.md) with all the objects you would like to add to the maintenance schedule, and then create or edit a maintenance schedule targeting the group(s). You can't include more than 216 group objects at a time.
>
>
> - The time zone specified for the Windows computer hosting the Management Server role will be applied to the maintenance schedule.
>
> - Changes to accommodate daylight savings time aren't automatically applied to maintenance schedules. You must manually edit the schedule to adjust for daylight savings time.
>
> - You can get historical data for when a monitored entity went into maintenance mode by querying the MaintenanceModeHistory table in the Operations Manager database.
>
> - The System Center Operations Manager SDK account must be a member of one of the following SQL Server roles in order to take advantage of the Maintenance Mode feature:
>
>   - SQLAgentUserRole
>   - SQLAgentReaderRole
>   - SQLAgentOperatorRole
>
>   For more information about setting the SDK action account, see [Account Information for Operations Manager](plan-security-accounts.md#system-center-configuration-service-and-system-center-data-access-service-account)

- The accounts that are listed under the Operational Database Account profile should have SQLAgentOperatorRole permission on the MSDB database.
- If any accounts that are listed under the Operational Database Account profile don't have access to the SQLAgentOperatorRole permission on the MSDB database, assign the SQLAgentOperatorRole permission on the MSDB database to each account under the Operational Database Account profile.
- If you don't have any accounts listed under the Operational Database Account profile, then the accounts that are available under the Default Action Account profile should have the SQLAgentOperatorRole permission on the MSDB database. This permission is granted automatically during the fresh installation of System Center Operations Manager 2019. However, in case of an upgrade to System Center Operations Manager 2019 from a previous version of System Center Operations Manager, this permission needs to be granted manually

To support the scenario of initiating maintenance mode directly from the agent-managed computer, Operations Manager now supports allowing a system administrator to set the machine in maintenance mode directly from the computer itself, without any need to perform it from the Operations console.  It can be performed with the new PowerShell cmdlet **Start-SCOMAgentMaintenanceMode**.  

The following section describes how to work with the different options for the on-demand maintenance mode feature.

## On-Demand Maintenance Mode

Select the required tab to work with the different options for the on-demand maintenance mode:

# [Put a monitored object into maintenance mode](#tab/MonitoredObject)

Follow these steps to put a monitored object into maintenance mode:

1. Sign in to the computer with an account that's a member of the Operations Manager Administrators role.

2. In the Operations console, select **Monitoring**.

3. In the **Monitoring** workspace, expand **Monitoring**, and select **Windows Computers**.

4. In the **Windows Computers** pane, right-click the windows computer that you want to place into maintenance mode, select **Maintenance Mode**, and select **Start Maintenance Mode**. You can use ctrl+click or shift+click to select multiple computers to place into maintenance mode.

5. In the **Maintenance Mode Settings** dialog, under **Apply to**, select **Selected objects only** if the computer is to be placed into maintenance mode; otherwise, select **Selected objects and all their contained objects**.

6. Select **Planned** if this is a planned event; otherwise, leave it cleared.

7. In the **Category** list, select the appropriate maintenance category.

8. Under **Duration**, select and enter the **Number of minutes** or select and enter the **Specific end time**, and select **OK**. A maintenance mode icon appears in the **Computers** pane, in the **Maintenance Mode** column for the computer you selected.

    > [!NOTE]
    > The minimum value for **Number of minutes** is 5. The maximum value is 1,051,200 (2 years).
    > To start the maintenance mode, the maximum wait time is 5 minutes.

# [Edit maintenance mode settings for a monitored object](#tab/Edit)

Follow these steps to edit the maintenance mode settings for a monitored object:

1. Sign in to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, select **Monitoring**.

3. In the **Monitoring** workspace, expand **Monitoring**, and select **Windows Computers**.

4. Right-click the computer in the **Windows Computers** pane whose settings you want to edit, select **Maintenance Mode**, and select **Edit Maintenance Mode settings**.

5. In the **Maintenance Mode Settings** dialog, edit the settings you want to change, and select **OK**.

# [Stop maintenance mode on a monitored object](#tab/Stop)

Follow these steps to stop the maintenance mode on a monitored object:

1. Sign in to the computer with an account that's a member of the Operations Manager Administrators role.

2. In the Operations console, select **Monitoring**.

3. In the **Monitoring** workspace, expand **Monitoring**, and select **Windows Computers**.

4. In the **Windows Computers** pane, right-click the computer that you want to take out of maintenance mode, select **Maintenance Mode**, and select **Stop Maintenance Mode**.

5. Do the following in the **Maintenance Mode** dialog:

    1. If you selected **Selected objects and all their contained objects** when you placed the computer into maintenance mode, select **Remove contained objects** and select **Yes**.

    2. If you selected **Selected objects only**, clear **Remove contained objects** and select **Yes**.

6. In the **Windows Computers** pane, the maintenance mode icon disappears from the **Maintenance Mode** column for the computer you selected.

    > [!NOTE]
    > Because Operations Manager polls maintenance mode settings only once every 5 minutes, there can be a delay in an object's scheduled removal from the maintenance mode.

---

::: moniker range="<sc-om-2019"

### Enable from Target System

Maintenance mode can be enabled directly from the monitored Windows computer by a systems administrator using the PowerShell cmdlet **Start-SCOMAgentMaintenanceMode**.  When a systems administrator or operator runs this PowerShell cmdlet on the computer, the command logs an event in the Operations Manager event log, and stores arguments for the maintenance activity such as duration, reason, comment, and information (like the time when the cmdlet was invoked).

The comment field contains user information, specifically who has invoked maintenance mode. A rule that targets the agent, runs every 5 minutes to read this registry entry on the agent with a PowerShell script  **ReadMaintenanceModeRegEntry.ps1**, and then marks this entry as invalid so at next invocation it won't pick this entry. The write action, which is part of the rule and targets the management server, takes this record and sets maintenance mode for the agent based on the record read from the registry.  The frequency the rule runs can be overridden to a custom interval.

::: moniker-end  

::: moniker range=">=sc-om-2019"

### Enable from Target System

Maintenance mode can be enabled directly from the monitored Windows computer by a server administrator using the PowerShell cmdlet **Start-SCOMAgentMaintenanceMode**. When server administrator or operator runs this PowerShell cmdlet on the computer, the command logs an event, which stores arguments for the maintenance mode, such as duration, reason, comment, and information like time of invocation of cmdlet.

A rule that targets the agent, reads the event entry on the agent and stores this in Operations Manager database. There's another rule *Microsoft.SystemCenter.Agent.MaintenanceMode.Trigger.Rule*, which runs every 4 minutes by default, and reads this event from the Operations Manager database. It then sets maintenance mode on the agent based on the record read from the event.

::: moniker-end

**Start-SCOMAgentMaintenanceMode** has the following syntax:

  ```PowerShell
  Start-SCOMAgentMaintenanceMode -Duration <Double (in minutes)> [-Reason <string>] [-Comments <string>]
  ```

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

1. To enable for an interval of five (5) minutes and with a major reason of **Planned** and minor reason **Other**, enter:

    `Start-SCOMAgentMaintenanceMode -Duration 5 –Reason PlannedOther`

2. To enable for an interval of 10 minutes with no reason, enter:

    `Start-SCOMAgentMaintenanceMode -Duration 10`

Perform the following steps to initiate maintenance mode from the target Windows computer:

1. Sign in to the computer.

2. On computers running Windows Server 2012 and higher, to run Windows PowerShell as an administrator from the **Start** screen, right-click the **Windows PowerShell** tile, and in the app bar, select **Run as administrator**.  

3. Change directory to the following path **C:\Program Files\Microsoft Monitoring Agent\Agent** by entering `cd C:\Program Files\Microsoft Monitoring Agent\Agent`.

4. Import the module MaintenanceMode.dll by entering `Import-module MaintenanceMode.dll`.

5. Enter **Start-SCOMAgentMaintenanceMode** and use the parameters to configure the maintenance mode request.

::: moniker range="<sc-om-2019"

> [!NOTE]  
> To confirm that the Maintenance Mode request is successful, you can look in the Operations Manager Event Log for an Event ID 2222 followed by one or more events with Event ID 1215. If Event ID 2222 is present but ID 1215 is missing, this indicates the maintenance mode request was missed. You'll need to re-raise the request.  
>
> In order to re-raise the request, you'll need to remove the record in the registry for the maintenance mode using the following command, and then re-run the **Start-SCOMAgentMaintenanceMode** cmdlet:
> `Set-ItemProperty -Path "HKLM:\software\Microsoft\Microsoft Operations Manager\3.0\MaintenanceMode" -Name record -Value "" `  

::: moniker-end

::: moniker range=">=sc-om-2019"

> [!NOTE]
> To confirm that maintenance mode request is successful, look in the Operations Manager system log for event ID 19999. In case event ID 19999 isn't available, submit the maintenance mode request again.

::: moniker-end

## Schedule maintenance mode

The following section describes how to work with the different options available for the maintenance mode scheduling feature.

### Create Maintenance Schedule in the Operations console

The following procedure describes how to create a maintenance schedule for selected monitored objects for a future date in the Operations console.  

1. Sign in to the computer with an account that's a member of the Operations Manager Administrators role.

2. In the Operations console, select **Monitoring**.

3. In the **Monitoring** workspace, expand **Monitoring**, and select **Maintenance Schedules**.

4. From the **Tasks** pane, select **Create Maintenance Schedule**.

5. In the **Create Maintenance Schedule** wizard, on the **Object Selection** page, select **Add/Remove objects...** and the **Create Group Wizard - Object Selection** dialog appears.

6. In the **Create Group Wizard - Object Selection** dialog, perform the following:

    1.  In the **Search for list**, the default item **Computer** is selected. Alternatively, you can select **Computer Group** or a specific class such as **SQL Server 2012 DB Engine** from the dropdown list.  

    2.  Optionally, in the **Filter by part of the name** box, enter all or part of the object name, and select **Search**.  

    3.  In the **Available items** box, select the desired objects, select **Add**, and select **OK**.

7. On the **Object Selection** page, select **Next**.

8. In the **Create Maintenance Schedule** wizard, on the **Schedule** page, you can specify the following for your maintenance schedule:

    1.  Choose the frequency as to how often you would like it to run.  If you select the option **Once**, the task will only run one time based on the start date and time selected.

    2.  Under **Duration** select the **Start Time** and for **End Time**, select the **number of minutes** or select and enter the **Specific end time**.  

    3.  Under **Schedule is effective beginning**, specify when this schedule is allowed to take effect and if you require it to no longer be valid after a period of time, select the option **The schedule expires on** and select a future expiration date.  

        > [!NOTE]
        > The minimum value for Number of minutes is 5. The maximum value is 1,051,200 (2 years).
        > To start the maintenance mode, the maximum wait time is 5 minutes.

9. Select **Next** once you've completed configuring the schedule options.

10. In the **Create Maintenance Schedule** wizard, on the **Details** page, specify the following:

    1.  Create a name for the schedule in the **Schedule Name** box.

    2.  Select **Planned** if this is a planned event; otherwise, leave it cleared.

    3.  In the **Category** list, select the appropriate maintenance category.

    4.  Select **Enable Schedule** if you want to enable the schedule now, or clear it if you plan on enabling the schedule later.

11. Select **Finish** to save your changes.  

The new schedule will appear in the list of maintenance schedules and you can edit, disable, or delete a maintenance schedule from the list. This can be accomplished by selecting the schedule from the list and choosing the corresponding option from the **Tasks** pane.

::: moniker range=">=sc-om-2019"

## Create maintenance schedule in the Web console

The following procedure describes how to create a maintenance schedule for selected monitored objects for a future date in the Web console.  

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console.

2. From the left pane in the Web console, select **Maintenance Schedules**.

3. From the top of the page, select **+ Create**.

4. In the **Create maintenance schedule** pane, perform the following:

    1.  In the **Search for classes**, the default item **Computer** is selected. Alternatively, you can select **Computer Group** or a specific class such as **SQL Server 2012 DB Engine** from the dropdown list.  

    2.  Optionally, in the **Filter by keyword** box, enter all or part of the object name, and then select **Enter**.  

    3. In the **Available objects** box, select the desired objects.

5. Expand **Schedule** and in this section, specify the following for your maintenance schedule:

    1.  Choose the frequency as to how often you would like it to run.  If you select the option **Once**, the task will only run one time based on the start date and time selected.

    2.  Under **Duration** select the **Start Time** and for **End Time**, select the **number of minutes** or select and enter the **Specific end time**.  

    3.  Under **Schedule is effective beginning**, specify when this schedule is allowed to take effect and if you require it to no longer be valid after a period of time, select the option **The schedule expires on** and select a future expiration date.  

        > [!NOTE]
        > The minimum value for Number of minutes is 5. The maximum value is 1,051,200 (2 years).
        > To start the maintenance mode, the maximum wait time is 5 minutes.

9. Expand **Completion** and in this section, specify the following to complete the configuration of your custom maintenance schedule:

    1.  Create a name for the schedule in the **Schedule Name** box.

    2.  From the **Category** dropdown list, select the appropriate maintenance category or leave it at the default of **other (Planned)**.

    3. Optionally, in the **Comment** box, enter a description for the scheduled maintenance task.  

    4.  Select **Enable Schedule** if you want to enable the schedule now, or clear it if you plan on enabling the schedule later.

7. Select **Finish** to save your changes.  

The new schedule will appear in the list of maintenance schedules and you can edit, disable, enable, or delete a maintenance schedule from the list.  This can be accomplished by selecting the schedule from the list and choosing the corresponding option from the menu at the top of the page.  

::: moniker-end  

::: moniker range=">=sc-om-2019"

## Enable scheduled maintenance mode with SQL Always On

In earlier releases of Operations Manager, maintenance schedules that targeted instances of SQL Server in an Always On availability group to provide high availability of the Operations Manager databases didn't work when failover to a replica on another SQL Server instance occurred. Operations Manager 2019 includes a fix for this issue to prevent this behavior, and ensures maintenance schedules work in a failover scenario.

**Guidelines**
- As  part of  fix for this issue, the existing schedules are converted to the new design. This happens automatically while upgrading to Operations Manager 2019.
- Any failures in the above operation are captured in the following database table:
  [OperationsManager].[dbo].[MaintenanceModeSchedulesMigrationLogs]
- Schedules that fail to get converted to the new design should be converted manually by executing the following scripts against the Operations Manager database.
    EXEC [dbo].[p_MaintenanceScheduleMigrateSchedule] \<ScheduleIDOftheMMSchedule\>
  Example:
    EXEC [dbo].[p_MaintenanceScheduleMigrateSchedule] '1A6917C6-999C-E811-837B-02155DC77B3F'
- To convert all the schedules to the new design, use the following command:
    Delete [OperationsManager].[dbo].[MaintenanceModeSchedulesMigrationLogs]
    EXEC [dbo].[p_MaintenanceScheduleMigrateExistingSchedules]

  >[!NOTE]
  >After you deploy the upgrade, maintenance schedules might be triggered and have a maximum delay of five (5) minutes. You can configure the maximum delay by overriding the **Maintenance Mode** rule. The default value five minutes is to avoid causing a large performance decrease on the system.

## Furthest end time during schedule overlap  

> [!NOTE]
> This feature is applicable from UR2 and later.

Currently, if there's a conflict in the maintenance mode window for object(s), the newly updated end time overwrites the existing scheduled time. If the latest defined time is longer than the previous value, then the computer stays in maintenance mode for an extended period. However, when the latest defined time is shorter, then the computer comes out of the maintenance mode earlier than expected, generating false alerts.

For example, user Dan schedules maintenance every Tuesday from **8AM – 3PM** on all the agents in Redmond. User Ryan creates another schedule post Dan to start the maintenance mode every Tuesday for all the agents running SQL server from **10AM-12PM**. There are 500 agents located in Redmond running SQL server, and now they'll exit maintenance mode at **12PM**, and Dan will receive false alerts and tickets for these agents.

False alerts generated by the above scenario can cost a lot of money, time, and delay in addressing the real issues for an organization. From Update Rollup 2, if multiple MM schedules are running for an object, the furthest end time will overwrite any other defined end time.

With 2019 UR2, if there's a conflict in maintenance mode end time, then the object will exit the maintenance mode at the furthest end time defined for the object. For the example above, servers, which are in Redmond and have SQL server, will exit maintenance mode at 3 PM, which is the furthest end time defined for them.

::: moniker-end

## Next steps

[Create and manage groups](manage-create-manage-groups.md)
