---
title: UNIX - Linux Shell Command Monitors
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70260657-2e1b-4e89-b501-cf7a8c3b2d5d
---
# UNIX - Linux Shell Command Monitors
UNIX\/Linux shell command monitors run on a schedule and execute a program or script, a command, or a one\-line command sequence \(using pipeline operators\). The output from the command is used to determine the health state of the target object. Shell command monitors are useful for custom monitoring of UNIX and Linux applications with information that is not accessible through other means.

## Options
When you run an UNIX\/Linux shell command monitor wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### Rule Type
The **Rule Type** page includes basic settings for the rule including its type and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Select the type of monitor to create|To create a shell command monitor that evaluates for two states \(healthy and error\), select **UNIX\/Linux Shell Command Two State Monitor**. <br />To create a shell command monitor that evaluates for three states \(healthy, warning and error\), select **UNIX\/Linux Shell Command Three State Monitor**.|
|Management Pack|Management pack file to store the rule or monitor.For more information on management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|

### General
The **General** page includes general settings for the rule including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Name|The name used for the monitor. This appears in the **Monitors** view in the **Authoring** pane. When you view the Health Explorer for the monitoring target, you can see the health state of this monitor.|
|Description|Optional description of the rule.|
|Monitor Target|The class to use for the target of the rule. The rule will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](./Understanding-Classes-and-Objects.md).|
|Parent Monitor|The aggregate monitor that this monitor will be placed under in the Health Explorer.|
|Monitor is enabled|If checked, the monitor is enabled and the shell command will run according to the schedule.<br />If unchecked, the monitor is not enabled and the script will not run. The monitor can be enabled for a group of target objects by creating an override to enable the monitor.|

### Schedule
The **Schedule** page defines the schedule to run the script. The script will run indefinitely according to this schedule until the monitor is disabled or deleted or the management pack is uninstalled.

|Option|Description|
|----------|---------------|
|Run every|Frequency that the script should be run. This should typically not be less than 5 minutes.|
|Synchronize at|If enabled, the schedule will be synchronized to occur at the specified time.|

### UNIX\/Linux Shell Command
The following options are available on the **Shell Command Details** page of the wizard.

|Option|Description|
|----------|---------------|
|Command|The shell command to execute. This can be the full path to a program or script, a command, or a one\-line sequence of multiple commands \(using pipeline operators\).|
|Run As Profile|Either the “UNIX\/Linux Action Account” or “UNIX\/Linux Privileged Account” profile. Select the profile that associates the required account credentials with the task target. The associated account will be used to execute the command.|
|Timeout \(seconds\)|The number of seconds that the command can run before the agent stops it. This prevents problem commands from running continuously and putting excess overhead on the agent computer.|

### Expressions
Each required expression for the monitor will have its own page in the wizard. A two\-state monitor will have the following expressions:

1.  Error Expression

2.  Healthy Expression

A three\-state monitor will have the following expressions:

1.  Error Expression

2.  Warning Expression

3.  Healthy Expression

> [!NOTE]
> Detailed information on expressions is available in [Expressions](./Expressions.md).

Each expression will typically compare the value of one or more of the properties from the command’s output to some value. Each expression must be different, and only one of the expressions should evaluate to True under any particular condition. In the next page of the wizard, you will associate each of the health states of the monitor with one of these expressions. When an expression evaluates to the True, the monitor will be set to that health state.

|Option|Description|
|----------|---------------|
|Parameter Name|The Parameter Name syntax for command execution output is:**StdOut**: \/\/\*\[local\-name\(\)\="StdOut"\]**StdErr**: \/\/\*\[local\-name\(\)\="StdErr"\]**Return Code**: \/\/\*\[local\-name\(\)\="ReturnCode"\]|
|Operator|The type of comparison to perform.|
|Value|The explicit value that should match the value in the property bag.|

### Configure Health
On this page, you map each of the expressions to a health state for the monitor. When a condition is true, the monitor is set to the health state that you define. For a three\-state monitor, you can typically accept the default settings. For a two\-state monitor, you typically only have to determine if the Unhealthy Expression should result in a Critical or Warning state.

|Option|Description|
|----------|---------------|
|Monitor Condition|Represents each of the expressions.|
|Health State|The health state to set the monitor to when that expression is true.|

### Configure Alerts

|Option|Description|
|----------|---------------|
|Generate alerts for this monitor|If checked, an alert will be created when the monitor changes from a healthy state to a warning or critical state, and all of the other options will be enabled.<br />If unchecked, the monitor will not generate alerts when the health state is changed, and all of the other options will be disabled.|
|Generate an alert when|For a two\-state monitor, this setting should be set to **The monitor is in a critical health state**.|
|Automatically resolve alert when the monitor returns to a healthy state|If checked, the alert will automatically be resolved when the monitor returns to a healthy state. If unchecked, the alert must be resolved manually.|
|Alert name|The name of the alert that is displayed in the console.|
|Alert Description|The description of the alert.|
|Priority|The priority of the alert: Low, Medium, or High.|
|Severity|The severity of the alert: Information, Warning, Critical, or matched to the health state of the monitor.|

## Creating an UNIX\/Linux Shell Command Monitor
The following procedure shows how to create a monitor based on a monitoring shell command with the following details:

-   Runs on any UNIX\/Linux computer every 15 minutes

-   Sets the monitor to a **Critical** state when the file “\/tmp\/error” exists.

-   Sets the monitor to a **Healthy** state when the file “\/tmp\/error" does not exist.

#### To create a two state UNIX\/Linux shell command monitor

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace, and then select **Monitors**.

3.  Launch the **Create a Monitor** task, and select **Unit Monitor**.

4.  On the **Monitor Type** page, do the following:

    1.  Expand **Scripting** and then expand **Generic**.

    2.  Select **UNIX\/Linux Shell Command Two State Monitor**.

    3.  In the **Management Pack** dropdown, select the management pack from step 1.

    4.  Click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Name** box, type **Error File Test Monitor.**

    2.  Click **Select** next to the **Monitor Target** box, select **UNIX\/Linux Computer**, and click **OK**.

    3.  Select the **Parent Monitor** of **Availability**.

    4.  Leave the **Monitor is enabled** box selected.

    5.  Click **Next**.

6.  On the **Schedule** page, do the following:

    1.  In the **Run every** box, type **15 minutes**.

    2.  Click **Next**.

7.  On the **Shell Command Details** page, do the following:

    1.  In the **Command** box, type **ls \/tmp\/error | wc –l**. This command sequence will return a 1 if the file “\/tmp\/error” exists, and a 0 if it does not.

    2.  In the **Run As Profile** box, select the **UNIX\/Linux Action Account** profile.

    3.  In the **Timeout \(Seconds\)** box, input **120**.

    4.  Click **Next**.

8.  On the **Error Expression** page, enter the following **And** expression:

    1.  **\/\/\*\[local\-name\(\)\=”StdOut”\] equals 1**

    2.  **\/\/\*\[local\-name\(\)\=”ReturnCode”\] equals 0**

9. On the **HealthyExpression** page, enter the following **And** expression:

    1.  **\/\/\*\[local\-name\(\)\=”StdOut”\] does not equal 1**

    2.  **\/\/\*\[local\-name\(\)\=”ReturnCode”\] equals 0**

10. On the **Configure Health** page, do the following:

    1.  Leave the **Health State** for the **StatusError** condition set to **Critical**.

    2.  Click **Next**.

11. On the **Configure Alerts** page, do the following:

    1.  Select **Generate alerts for this monitor**.

    2.  In the **Generate an alert when** box, select **The monitor is in a critical health state**.

    3.  Leave the box selected to automatically resolve the alert.

    4.  In the **Alert name** box, type **Application test failed**.

    5.  Clear the existing text in the **Alert description** box and type **Computer:**

    6.  Click the ellipse button.

    7.  Click **Target** and then select **Network Name**.

    8.  Click **OK**.

    9. In the **Alert description** box, add a new line and type **StdOut: $Data\/Context\/\/\/\*\[local\-name\(\)\=”StdOut”\]$**

12. Click **Create**.

## See Also
[Script Monitors and Rules](./Script-Monitors-and-Rules.md)


