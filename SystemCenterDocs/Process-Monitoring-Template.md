---
title: Process Monitoring Template
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 684a5a24-ce65-43b8-af8e-4ade060acf6e
---
# Process Monitoring Template
The *Process Monitoring* template lets you monitor whether a particular process is running on a computer. By using this template, you can implement two different basic scenarios: You might require the process to be running for a particular application and want to be warned if it is not running, or you might have to be alerted if you discover that an unwanted process is running. In addition to monitoring whether the application is running, you can collect performance data for the processor and memory usage of the process.

## Scenarios
Use the **Process Monitoring** template in different scenarios where you have to monitor a running process on an agent\-managed Windows\-based computer. Your application can monitor the following processes.

### Critical Process
A process that must be running at all times. Use the **Process Monitoring** template to ensure that this process is running on the computers where it is installed, and use the **Process Monitoring** template to measure its performance.

### Unwanted Process
A process that should not be running. This process might be a known rogue process that can cause damage, or it might be a process that is automatically started when an error in the application occurs. The **Process Monitoring** template can monitor for this process and send an alert if it is found to be running.

### Long Running Process
A process that runs for short periods at a time. If the process is running for an excessive length of time, it might indicate a problem. The **Process Monitoring** template can monitor for the length of time that this process runs and send an alert if the running time exceeds a particular duration.

## Monitoring Performed by Process Monitoring Template
Depending on your selections in the Process Monitoring wizard, the monitoring performed by the created monitors and rules can include any of the following settings.

|Type|Description|When Enabled|
|--------|---------------|----------------|
|Monitors|Count of wanted processes running|Enabled if you select **Processes you want** on the **Process to Monitor** page and **Number of processes** on the **Running Processes** page.|
|Monitors|Time that a wanted process has been running|Enabled if you select **Processes you want** on the **Process to Monitor** page and **Duration** on the **Running Processes** page.|
|Monitors|Unwanted process running|Enabled if **Monitoring Scenario** is for unwanted processes.|
|Monitors|Processor utilization of process|Enabled if you select **Processes you want** on the **Process to Monitor** page, and you enable **CPU alert** on the **Performance Data** page.|
|Monitors|Memory usage of process|Enabled if you select **Processes you want** on the **Process to Monitor** page, and you enable **memory alert** on the **Performance Data** page.|
|Collection Rules|Collection of processor utilization of process|Enabled if you select **Processes you want** on the **Process to Monitor** page, and you enable **CPU alert** on the **Performance Data** page.|
|Collection Rules|Collection of memory usage of process.|Enabled if you select **Processes you want** on the **Process to Monitor** page, and you enable **memory alert** on the **Performance Data** page.|

## Viewing Monitoring Data
All data collected by the **Process Monitoring** template is available in the **Process State** view located in the **Windows Service and Process Monitoring** folder. In this view, an object is listed for each agent in the group that you selected. Even if an agent does not monitor a process, it is listed, and the monitor reflects the state for the process that is not running.

You can view the state of the individual process monitors by opening the [!INCLUDE[om12short](./Token/om12short_md.md)] Health Explorer for the process object. You can view performance data by opening the Performance view for the process object.

The same process objects that are listed in the **Process State** view are included in the Health Explorer for the computer that hosts the process. The health state of the process monitors rolls up to the health of the computer.

## <a name="Options"></a>Wizard Options
When you run the **Process Monitoring** template, you have to provide values for the options in the following tables. Each table represents a single page in the wizard.

### General Properties
The following options are available on the **General Options** page of the wizard.

|Option|Description|
|----------|---------------|
|Name|The name used for the process. This name is displayed in the Operations console for the wizard. It does not have to be the same name as the process.|
|Description|Optional description of the process.|
|Management Pack|Management pack to store the class and monitors that the template creates. If you create any additional monitors or rules that are using the service as a target class, they have to be stored in the same management pack.<br /><br />For more information about management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|

### Process to Monitor
The following options are available on the **Process to Monitor** page of the wizard.

|Option|Description|
|----------|---------------|
|Monitoring Scenario|The kind of monitoring that is to be performed. Select **Monitor whether and how a process is running** to monitor for a wanted process and set the monitor to a critical state when the process is not running. Select **Monitor only whether a process is running** to monitor for an unwanted process and set the monitor to a critical state when the process is running.|
|Process name|The full name of the process. This is the name of the process as it appears in Task Manager. It should not include the path to the actual executable file. You can either type the name or click the ellipse \(**…**\) button to locate the file name.|
|Targeted group|The process is monitored on all computers that are included in the specified group.|

### Running Processes
The following options are available on the **Running Processes** page of the wizard.

|Option|Description|
|----------|---------------|
|Generate an alert of the number of processes is below the minimum value or above the maximum value for longer than the specified duration|If selected, the monitor is set to a critical state, and an alert is created if the number of instances of the specified process is less than the specified minimum or greater than the specified maximum for a longer period than the specified duration.<br /><br />To ensure that at least one instance of the process is running, set both the minimum and maximum to 1.|
|Minimum number of processes|The minimum number of processes that should be running.|
|Maximum number of processes|The maximum number of processes that should be running.|
|Duration|Specifies how long the number of running processes must exceed the specified range before the monitor is set to a critical state. Do not set this value to less than 1 minute.|
|Generate an alert if the process runs longer than the specified duration|If selected, the monitor is set to a critical state, and an alert is created if one instance of the process runs for longer than the specified duration.|

### Performance Data
The following options are available on the **Performance Data** page of the wizard.

|Option|Description|
|----------|---------------|
|Generate an alert if CPU usage exceeds the specified threshold|Specifies if CPU usage of the process should be monitored. A monitor will be created to set an error state on the object and generate an alert when the specified threshold is exceeded. A rule is created to collect CPU usage for analysis and reporting.|
|CPU Usage \(percentage\)|If CPU utilization is monitored, this option sets the threshold. If the percentage of total CPU usage exceeds the threshold, the object is set to an error state, and an alert is generated.|
|Generate an alert if memory usage exceeds the specified threshold|Specifies if memory usage of the process should be monitored. A monitor will be created to set an error state on the object, and generate an alert when the specified threshold is exceeded. A rule is created to collect CPU usage for analysis and reporting.|
|Memory Usage \(MB\)|If memory usage is monitored, this option sets the threshold. If the disk space in megabytes \(MB\) of total CPU usage exceeds the threshold, the object is set to an error state, and an alert is generated.|
|Number of samples|If CPU usage or memory is monitored, this option specifies the number of consecutive performance samples that must be exceeded before the object is set to an error state, and an alert is generated.<br /><br />Specifying a number greater than 1 for this option limits the noise from monitoring by ensuring that an alert is not generated when the service only briefly exceeds the threshold. The larger the value that you set, the longer the period of time before you are alerted to a problem. A typical value is 2 or 3.|
|Sampling interval|If CPU usage or memory is monitored, specify the length of time between performance samples.<br /><br />A smaller value for this option reduces the time for detecting a problem but increases overhead on the agent and the amount of data collected for reporting. A typical value is between 5 and 15 minutes.|

### Additional Monitoring
In addition to performing the specified monitoring, the **Process Monitoring** template creates a targetd class that you can use for additional monitors and workflows. Any monitor or rule using this class as a target will run on any agent\-managed computer in the group specified in the template. If it creates Windows events that indicate an error, for example, you could create a monitor or rule that detects the particular event and uses the process’ class as a target.

### Creating and Modifying Process Monitor Templates

##### To run the Process Monitoring wizard

1.  Determine the target group for the monitor by using the following logic:

    -   If you want to discover the process on all Windows\-based computers in the management group, you do not have to create a group. You can use the existing group **All Windows Computers**.

    -   If you only want the process to be discovered on a certain group of computers, either ensure that an appropriate group exists or create a new group by using the procedure in [How to Create Groups in Operations Manager](./How-to-Create-Groups-in-Operations-Manager.md).

    -   If the process that you are monitoring is in a cluster, create a group with objects of the class **Virtual Server** representing the nodes of the cluster that contain the service.

2.  Start the Add Monitoring wizard.

3.  On the **Select Monitoring Type** page, select **Process Monitoring**, and then click **Next**.

4.  On the **General Properties** page, in the **Name** and **Description** boxes, type a name and an optional description. The name is used to describe the process in the Operations console. It is not the actual name of the process.

5.  Select a management pack in which to save the monitor, or click **New** to create a new management pack. For more information, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

6.  Click **Next**.

7.  On the **Process to Monitor** page, do the following:

    1.  Select whether you want to monitor a **wanted** or an **unwanted** process.

    2.  In the **Process name** box, type the complete name of the process to monitor. For example, **notepad.exe**. You can also click the ellipse **\(…\)** button and locate the executable file.

    3.  Click the ellipse **\(…\)** button to the right of the **Targeted Group** box, and then select the group from the first step of this procedure.

    4.  Click **Next**.

8.  If you selected the option for a **wanted** process, on the **Running Processes** page, do the following:

    1.  If you want to monitor whether the process is running, do the following:

        1.  Select the option to **Generate an alert of the number of processes is below the minimum value or above the maximum value for longer than the specified duration**.

        2.  In the **Minimum number of processes** box, enter the minimum number of processes that should be running. For a single instance of the process, this is typically 1.

        3.  In the **Maximum number of processes** box, enter the maximum number of instances of the process that should be running.

        4.  In the **Duration** box, enter the length of time that running processes must exceed the specified range before the monitor is set to a critical state. This value should not be set to less than 1 minute. Note that the process could stop and restart within this time window with no error detected.

    2.  If you want to monitor for the length that a process runs, do the following:

        1.  Select the option to **Generate an alert if the process runs longer than the specified duration**.

        2.  In the **Duration** box, enter the maximum length of time that you want the process to run before the monitor is set to a critical state. This value should not be set to less than 1 minute.

9. If you selected the option for a wanted process, on the **Performance Data** page, select the performance counters and thresholds that you want to monitor. For more detailed information, see the [Wizard Options](./Process-Monitoring-Template.md#Options) section.

    > [!NOTE]
    > This page is disabled if you selected the option for an **unwanted** process.

10. If you have selected performance counters, specify the monitoring interval.

11. Click **Next**.

12. Review the summary of the monitor, and then click **Create**.

##### To modify an existing Process Monitoring template

1.  Open the Operations console with a user account that has Author credentials.

2.  Open the **Authoring** workspace.

3.  In the **Authoring** navigation pane, expand **Management Pack Templates**, and then click **Process Monitoring**.

4.  In the **Process Monitoring** pane, locate the monitor to change.

5.  Right\-click the monitor, and then select **Properties**.

6.  Enter the changes that you want, and then click **OK**.

### Viewing Process Monitoring Monitors and Collected Data

##### To view all Process Monitoring monitors

1.  Open the Operations console.

2.  Open the **Monitoring** workspace.

3.  In the **Monitoring** navigation pane, select **Windows Service and Process Monitoring**, and then click **Process State**.

##### To view the state of each monitor

1.  In the **Process State** pane, right\-click an object. Select **Open**, and then click **Health Explorer**.

2.  Expand the **Availability** and **Performance** nodes to view the individual monitors.

##### To view the performance collected for a process

1.  In the **Process State** pane, right\-click an object. Select **Open**, and then click **Performance**.

2.  In the **Legend** pane, select the counters that you want to view.

3.  Use options in the **Actions** pane to modify the Performance view.

## See Also
[Creating Management Pack Templates](./Creating-Management-Pack-Templates.md)
[Watcher Nodes](./Watcher-Nodes.md)


