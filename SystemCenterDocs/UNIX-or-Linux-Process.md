---
title: UNIX or Linux Process
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bca73ff2-ae75-42d0-9b12-ef37f98e1c7a
---
# UNIX or Linux Process
The *UNIX\/Linux Process Monitoring* template lets you monitor that a particular process installed on an UNIX or Linux computer runs.

## Scenarios
The **UNIX\/Linux Process Monitoring** template is useful for monitoring any application as monitoring processes is typically critical to the health of the application.

## Monitoring Performed by the UNIX\/Linux Process Monitoring Template
The following table shows the monitoring activity that the **UNIX\/Linux Process Monitoring** template performs.

|Type|Description|When Enabled|
|--------|---------------|----------------|
|Monitors|Process Count is Outside of Range|Always enabled.|

## <a name="Options"></a>Wizard Options
When you run the **UNIX\/Linux Process Monitoring** template, you have to provide values for options in the following tables. Each table represents a single page in the wizard.

### General Options
The following options are available on the **General Options** page of the wizard.

|Option|Description|
|----------|---------------|
|Name|The name used for the template. This is the name that is displayed in the Operations console.|
|Description|Optional description of the template.|
|Management Pack|Management pack to store the class and monitors that the template creates. If you create any additional monitors or rules that are using the process as a targeted process, you must store them in the same management pack.<br /><br />For more information about management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|

### Process Monitoring Details
The following options are available on the **Process Monitoring Details** page of the wizard.

|Option|Description|
|----------|---------------|
|Process name|The name of the process. You can use the **Select a Process** button to connect to a monitored UNIX\/Linux computer and list current running processes in order to select a process by name. If you wish to target the monitor to only a single computer, you must use the **Select a Process** button to select a computer and process.|
|Computer Group|The name of the group of UNIX or Linux computers for the process to monitor. Click the **Select a group** button to select a group that is installed in your management group. If you have used the **Select a Process** button to select a running process from a computer, the monitor will be targeted to that computer. After using the **Select a Process** button to select a process, you can use the **Select a Group** button to target a group with the monitor for the selected process.|
|Alert Severity|The severity for the alert:  Error, Warning, or Information.|
|Regular Expression to filter process arguments|An optional Regular expression to use in filtering processes by arguments. If this option is used, processes that match the provided process name will be additionally filtered by their arguments. Only processes with arguments that match the Regular expression will be evaluated by the monitor. This is useful to identify a process for a specific application when other applications on the system may use a process with the same name. The Regular expression is evaluated against a concatenated list of process arguments.|
|Expression Matching Results|If you use the **Select a Process** button to connect to a monitored computer and select a process by name, the list of all processes with the selected process name for that computer are shown in this field. When you provide a **Regular expression to filter process arguments** the processes listed in this field are filtered so that you can preview the filtering by argument.|

### Process Template Settings
The following options are available on the **Process Template Settings** page of the wizard.

|Option|Description|
|----------|---------------|
|Minimum number of instances|The minimum number of running instances of the monitored process. To alert if no instances of the process are running, check the box **Generate an alert when the number of process instances is less than the specified value**, and input a value of 1. The number of process instances is calculated after filtering by process name and the optional Regular expression to filter process arguments. If the number of running instances is less than the provided value, an alert will be generated.|
|Maximum number of instances|The maximum number of running instances of the monitored process. To alert if more than a specific number of instances of the process are running, check the box **Generate an alert when the number of process instances is greater than the specified value**, and input the maximum threshold value. The number of process instances is calculated after filtering by process name and the optional Regular expression to filter process arguments. If the number of running instances is greater than the provided value, an alert will be generated.|

## Additional Monitoring
In addition to performing the specified monitoring, the **UNIX\/Linux Process Monitoring** template creates a target class that you can use for additional monitors and rules. Any monitor or rule that uses this class as a target  runs on any agent where the process is installed.

### Creating and Modifying UNIX\/Linux Process Monitoring Templates

##### To create a UNIX\/Linux Process Monitoring template

1.  If you want to monitor a process on a group of computers, determine the targeted group for the monitor by using the following logic:

    -   If you want to discover the process on all UNIX and Linux computers in the management group, you do not have to create a group. You can use the existing group **UNIX\/Linux Computer Group**.

    -   If you only want the process to be discovered on a certain group of computers, then either ensure that an appropriate group exists or create a one by using the procedure in [How to Create Groups in Operations Manager](./How-to-Create-Groups-in-Operations-Manager.md).

2.  Start the **Add Monitoring** wizard.

3.  On the **Select Monitoring Type** page, select **UNIX\/Linux Process Monitoring**, and then click **Next**.

4.  On the **General Properties** page, in the **Name** and **Description** boxes, type a name and optional description for this new template.

5.  Select a management pack in which to save the monitor or click **New** to create a new management pack. For more information, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

6.  Click **Next**.

7.  Click the **Select a Process** button.

8.  Click the **Browse** button and select a computer that has the process installed, and then click **OK**.

9. In the **Processes** box, select the process to monitor.

10. Select an **Alert Severity**.

11. Optionally, provide a Regular expression to filter the matched process list by process arguments, in the field **Regular expression to filter process arguments**.

12. If you want to monitor the process on a group of computers, do the following:

    1.  Click the **Select a Group** button.

    2.  Select a group that contains the computers with the process, and then click **OK**.

13. Click **Next**.

14. Check the appropriate boxes for **Generate an alert when the number of process instances is less than the specified value** and **Generate an alert when the number of process instances is greater than the specified value**.

15. Provide values for **Minimum number of instances** and **Maximum number of instances**, if appropriate.

16. Click **Next**.

17. Click **Create**.

##### To modify an existing UNIX\/Linux Process Monitoring template

1.  Open the Operations console with a user account that has Author credentials.

2.  Open the **Authoring** workspace.

3.  In the **Authoring** navigation pane, expand **Management Pack Templates**, and then select **UNIX\/Linux Process Monitoring**.

4.  In the **UNIX\/Linux Process Monitoring** pane, locate the template to change.

5.  Right\-click the template, and then select **Properties**.

6.  Enter the changes that you want, and then click **OK**.

### Viewing UNIX\/Linux Process Monitors and Collected Data

##### To view the state of each monitor

1.  Select the **UNIX\/Linux Computers** view.

2.  In the **UNIX\/Linux Computers** pane, right\-click an object, select **Open**, and then click **Health Explorer**.

3.  Expand the **Availability** node, and then click the **Application\/Service Availability Rollup** node to view the individual process monitor.

## See Also
[Creating Management Pack Templates](./Creating-Management-Pack-Templates.md)


