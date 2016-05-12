---
title: Script Monitors_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f2e63f5-2225-49a3-b532-f0db4e236272
---
# Script Monitors_1
Script monitors run a script on a schedule and use its output to determine the health state of the target object. Script monitors are useful for performing test transactions against applications or gathering information that is not accessible through other means. The results of the script are returned in a [Property Bags](Script-Monitors-and-Rules.md#PropertyBags) that are evaluated against criteria to determine the resulting health state.

\[Conceptual view of script monitor\]

## Options
When you run a script monitor wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General

|Option|Description|
|----------|---------------|
|Name|The name used for the monitor. This appears in the Health Explorer for each target object.|
|Description|Optional description of the monitor.|
|Management Pack|Management pack to store the classes, monitors, and rules created by the template.<br /><br />For more information on management packs, see [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).|
|Monitor target|The class to use for the target of the monitor. The monitor will be run on any agent that has at least one instance of this class, and the health of those objects will be affected by the health of this monitor. For more information on targets, see [Understanding Classes and Objects](Understanding-Classes-and-Objects.md).|
|Parent Monitor|The aggregate monitor that this monitor will be placed under in the Health Explorer.|
|Monitor is enabled|If checked, the monitor is enabled and the script will run according to the schedule.<br /><br />If unchecked, the monitor is not enabled and the script will not run. The monitor can be enabled for a group of target objects by creating an override to enable the monitor.|

### Schedule
The **Schedule** page defines the schedule to run the script. The script will run indefinitely according to this schedule until the monitor is disabled or deleted or the management pack is uninstalled.

|Option|Description|
|----------|---------------|
|Run every|Frequency that the script should be run. This should typically not be less than 5 minutes.|
|Synchronize at|If enabled, the schedule will be synchronized to occur at the specified time.|

### Script
The **Script** page contains the body of the script itself and its parameters. You can type the script directly into the dialog box, but you will usually write it using another text editor and then copy the text of the script and paste it. This allows you to use a more functional editing tool and test the script on a command line before including it in the management pack.

|Option|Description|
|----------|---------------|
|File Name|Name of the script. Must have either a .vbs or .js extension depending on its language. There is no requirement to make this name unique because each script is provided its own temporary directory on the agent.|
|Timeout|The number of seconds that the script can run before the agent stops it. This prevents problem scripts from running continuously and putting excess overhead on the agent computer.<br /><br />The timeout value assigned to a script should allow enough time for the script to run under ordinary conditions, but should be less than the interval that the script is scheduled to run. If a script is configured to have a timeout value greater than its duration, then possibly multiple copies of the script could be running concurrently.|
|Script|The body of the script.|
|Parameters|Click to provide values for any arguments in the script. For more information, see [Script Arguments](Script-Monitors-and-Rules.md#ScriptArguments).|

### Expressions
Each required expression for the monitor will have its own page in the wizard. A two state monitor will have the following expressions:

-   Unhealthy Expression

-   Healthy Expression

A three state monitor will have the following expressions:

-   Unhealthy Expression

-   Degraded Expression

-   Healthy Expression

> [!NOTE]
> Detailed information on expressions is available in [Expressions](Expressions.md).

Each expression will typically compare the value of one or more of the properties from the script’s property bag to some value. Each expression must be different, and only one of the expressions should evaluate to True under any particular condition. In the next page of the wizard, you will associate each of the health states of the monitor with one of these expressions. When an expression evaluates to the True, the monitor will be set to that health state.

For example, the script might perform a test transaction against a particular application and return a single property with a value of “Good” if the transaction completed successfully, and “Bad” if the transaction failed.

|Option|Description|
|----------|---------------|
|Parameter Name|This will be a $Data variable representing the particular value that you need from the property bag. This will be in the following syntax:<br /><br />Property\[@Name\="PropertyName"\]|
|Operator|The type of comparison to perform.|
|Value|The explicit value that should match the value in the property bag.|

### Configure Health
On this page, you map each of the expressions to a health state for the monitor. When a condition is true, the monitor is set to the health state that you define. For a three state monitor, you can typically accept the default settings. For a two state monitor, you typically only have to determine if the Unhealthy Expression should result in a Critical or Warning state.

|Option|Description|
|----------|---------------|
|Monitor Condition|Represents each of the expressions.|
|Health State|The health state to set the monitor to when that expression is true.|

### Configure Alerts

|Option|Description|
|----------|---------------|
|Generate alerts for this monitor|If checked, an alert will be created when the monitor changes from a healthy state to a warning or critical state, and all of the other options will be enabled.<br /><br />If unchecked, the monitor will not generate alerts when the health state is changed, and all of the other options will be disabled.|
|Generate an alert when|For a two\-state monitor, this setting should be set to **The monitor is in a critical health state**.|
|Automatically resolve alert when the monitor returns to a healthy state|If checked, the alert will automatically be resolved when the monitor returns to a healthy state. If unchecked, the alert must be resolved manually.|
|Alert name|The name of the alert that is displayed in the console.|
|Alert Description|The description of the alert.|
|Priority|The priority of the alert: Low, Medium, or High.|
|Severity|The severity of the alert: Information, Warning, Critical, or matched to the health state of the monitor.|

## Creating a Script Monitor
The following procedure shows how to create a monitor based on a monitoring  script with the following details:

The monitor created in this procedure has the following characteristics:

-   Runs on any computer with an instance of a particular service installed.

-   Sets the monitor to a **critical** state when the script returns a status message of Bad.

-   Sets the monitor to a **healthy** state when the script returns a status message of Good.

-   The script accepts an argument for the computer name of the target object’s agent and for an argument specifying wherther thereturns a Good or Bad message.

-   The script itself is only for testing and performs no real function. It simulates a script running a synthetic transaction.

#### To create a two state script monitor

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace, and then select **Monitors**.

4.  In the **Monitors** pane, click **Change Scope** and then select the name of the target that you created in step 2.

5.  Expand the target class then expand **Entity Health**.

6.  Right\-click **Availability**, select **Create a Monitor**, and then select **Unit Monitor**.

7.  On the **Monitor Type** page, do the following:

    1.  Expand **Scripting** and then expand **Generic**.

    2.  Select **Timed Script Two State Monitor**.

    3.  In the **Management Pack** dropdown, select the management pack from step 1.

    4.  Click **Next**.

8.  On the **General** page, do the following:

    1.  In the  **Name** box, type **My Application Script Monitor**.

    2.  The **Monitor target** box should already have the correct target class.

    3.  **Parent Monitor** box should already have **Availability**.

    4.  Leave the **Monitor is enabled** box selected.

    5.  Click **Next**.

9. On the **Schedule** page, do the following:

    1.  In the **Run every** box, type **15 minutes**.

    2.  Click **Next**

10. On the **Script** page, do the following:

    1.  For the **File Name** value, type **MyScript.vbs**

    2.  For the **Timeout** value, type **1 minutes**

    3.  In the **Script** box, paste the complete contents of the following script.

        ```vbs

        sComputerName = WScript.Arguments(0)
        bTestSuccessful = WScript.Arguments(1)

        Set oAPI = CreateObject("MOM.ScriptAPI")
        oAPI.LogScriptEvent "MyScript.vbs",10,4, "Running script on " & sComputerName
        Set oBag = oAPI.CreatePropertyBag()
        Call oBag.AddValue("ComputerName",sComputerName)
        If bTestSuccessful = True Then
           Call oBag.AddValue("Result","Good")
        Else
           Call oBag.AddValue("Result","Bad")
        End If
        oAPI.Return(oBag)

        ```

    4.  Click the **Parameters** button.

    5.  Select **Target**, then select **\(Host\=Windows Computer\)**, then select **Principal Name \(Windows Computer\)**.

    6.  Type a space after the Principal Name variable and then type **False**.

    7.  Click **OK**.

    8.  Click **Next**.

11. On the **Unhealthy Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **Property\[@Name\='Result'\]**.

    3.  In the **Operator** box select **Equals**.

    4.  In the **Value** box type **Bad**.

    5.  Click **Next**.

12. On the **Healthy Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **Property\[@Name\='Result'\]**.

    3.  In the **Operator** box select **Equals**.

    4.  In the **Value** box type **Good**.

    5.  Click **Next**.

13. On the **Configure Health** page, do the following:

    1.  Change the **Health State** for the Unhealthy condition to **Critical**.

    2.  Click **Next**.

14. On the **Configure Alerts** page, do the following:

    1.  Select **Generate alerts for this monitor**

    2.  In the **Generate an alert when** box, select **The monitor is in a critical health state**.

    3.  Leave the box selected to automatically resolve the alert.

    4.  In the **Alert name** box, type **Application test failed.**

    5.  Clear the existing text in the **Alert description** box and type **Result:**

    6.  Click the ellipse button.

    7.  Click **Data** and then **Property**.

    8.  Replace **<<STRING>>** with **Result**.

    9. Click **OK**.

15. Click **Create**.

## See Also
[Script Monitors and Rules](Script-Monitors-and-Rules.md)


