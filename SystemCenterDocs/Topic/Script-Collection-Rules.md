---
title: Script Collection Rules
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 548dcbc6-3846-4d08-9268-c55de8fbdf57
---
# Script Collection Rules
Script collection rules run a script on a schedule and store its output as either performance data or an event. As part of creating the rule, you need to specify which property bag values from the script or properties from the target object that will be used for different properties of the event or performance data being created.

## Options
When you run the script collection wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General

|Option|Description|
|----------|---------------|
|Rule Name|The name used for the rule. This appears in the **Rules** view in the **Authoring** pane.|
|Description|Optional description of the rule.|
|Management Pack|Management pack to store the monitor.<br /><br />For more information on management packs, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).|
|Rule Category|The category for the rule. For an event collection rule, this should be **Event Collection**. For a performance collection rule, this should be **Performance Collection**.|
|Rule target|The class to use for the target of the rule. The rule will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](../Topic/Understanding-Classes-and-Objects.md).|

### Schedule
The **Schedule** page defines the schedule to run the script. The script will run indefinitely according to this schedule until the rule is disabled or deleted or the management pack is uninstalled.

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
|Parameters|Click to provide values for any arguments in the script. For more information, see [Script Arguments](../Topic/Script-Monitors-and-Rules.md#ScriptArguments).|

### Performance Mapper \(Performance Collection Only\)
The **Performance Mapper** page is used to define values for the properties of the performance data being collected.

|Option|Description|
|----------|---------------|
|Object|Text for the Object name. This is required.|
|Counter|Text for the Counter name. This is required.|
|Instance|Text for the Instance name. This only required if the target of the rule has multiple instances.|
|Value|Numeric for the value for the performance|

### Event Mapper \(Event Collection Only\)
The **Event Mapper** page is used to define values for the properties of the event that will be collected. The value for each field will either be an explicit string of text, a value from the property bag of the script, or the value of a property of the target object.

|Option|Description|
|----------|---------------|
|Computer|The name of the computer that the event was logged on. This will usually be a $Target variable for the Principal Name of the computer. You can select this value by clicking on the ellipse button next to the text box.|
|Event source|The source of the event. This will usually be an explicit value but may be a $Data variable to use the value of a property from the script.|
|Event log|The name of the event log. This will usually may be an explicit value or a $Data variable to use the value of a property from the script.|
|Event ID|The numeric event number. This will usually be an explicit value or a $Data variable to use the value of a property from the script.|
|Category|The value of the EventCategory parameter \(an integer from 0 to 65535\) is an index into a category dynamic\-link library \(DLL\) message table that contains a localized string. Each publisher defines its own set of categories. These categories commonly correspond to individual components \(for example: a connector, module host, or data warehouse\).|
|Level|The severity of the event. You can select this value from the drop down list.|

## Creating Script Collection Rules
The following procedure creates a performance script collection rule with the following details:

-   Runs on any computer with an instance of a particular service installed.

-   The script accepts two parameters, one for computer name and another for the version of the application that is stored as a property on the target class.

-   The script itself is only for testing and performs no real function. It simulates a script running a synthetic transaction and returning a property bag with static values.

#### To create a script based performance collection rule

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](../Topic/Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

4.  Right\-click **Rules** and select **Create a new rule**.

5.  On the **Rule Type** page, do the following:

    1.  Expand **Collection Rules**, then expand **Probe Based**, and then select **Script \(Performance\)**.

    2.  In the **Management Pack** dropdown, select the management pack from step 1.

    3.  Click **Next**

6.  On the **General** page, do the following:

    1.  In the **Rule name** box, type **My Application Collect Script Performance**.

    2.  In the **Rule Category** drop down box, select **Performance Collection**.

    3.  Click **Select**.

    4.  Select the name of the target you created in step 2.

    5.  Click **OK**.

7.  On the **Schedule** page, do the following:

    1.  In the **Run every** box, type **15 minutes**.

    2.  Click **Next**

8.  On the **Script** page, do the following:

    1.  For the **File Name** value, type **MyPerfCollectionScript.vbs**

    2.  For the **Timeout** value, type **1 minutes**

    3.  In the **Script** box, paste the complete contents of the following script.

        ```vbs

        sComputerName = WScript.Arguments(0)
        sVersion = WScript.Arguments(1)

        [oAPI.LogScriptEvent]
        Set oAPI = CreateObject("MOM.ScriptAPI")
        Set oBag = oAPI.CreatePropertyBag()
        Call oBag.AddValue("ComputerName",sComputerName)
        Call oBag.AddValue("InstanceName","MyInstance")
        Call oBag.AddValue("Value",10)

        oAPI.Return(oBag)

        ```

    4.  Click the **Parameters** button.

    5.  Select **Target**, select **\(Host\=Windows Computer\)**, and then select **Principal Name \(Windows Computer\)**.

    6.  Type a SPACE.

    7.  Select **Target** and then **Version \(My Computer Role Base\)**.

    8.  Click **OK**.

    9. Click **Next**.

9. On the **Performance Mapper** page, do the following:

    1.  In the **Object** box type **MyApplication**.

    2.  In the **Counter** box type **MyCounter**.

    3.  In the **Instance** box type **$Data\/Property\[@Name\=FileName\]$**.

    4.  In the **Value** box type **$Data\/Property\[@Name\=’FileSize’\]$**.

    5.  Click **Create**.

The following procedure creates an event script collection rule with the following details:

-   Runs on any computer with an instance of a particular service installed.

-   The script accepts two parameters, one for computer name and another for the version of the application that is stored as a property on the target class.

-   The script itself is only for testing and performs no real function. It simulates a script running a synthetic transaction and returning a property bag with static values.

#### To create a script based event collection rule

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](../Topic/Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

4.  Right\-click **Rules** and select **Create a new rule**.

5.  On the **Rule Type** page, do the following:

    1.  Expand **Collection Rules**, then expand **Probe Based**, and then select **Script \(Event\)**.

    2.  In the **Management Pack** dropdown, select the management pack from step 1.

    3.  Click **Next**

6.  On the **General** page, do the following:

    1.  In the **Rule name** box, type **My Application Collect Script Event**.

    2.  In the **Rule Category** drop down box, select **Event Collection**.

    3.  Click **Select**.

    4.  Select the name of the target you created in step 2.

    5.  Click **OK**.

7.  On the **Schedule** page, do the following:

    1.  In the **Run every** box, type **15 minutes**.

    2.  Click **Next**

8.  On the **Script** page, do the following:

    1.  For the **File Name** value, type **MyEventCollectionScript.vbs**

    2.  For the **Timeout** value, type **1 minutes**

    3.  In the **Script** box, paste the complete contents of the following script.

        ```vbs

        sComputerName = WScript.Arguments(0)
        sVersion = WScript.Arguments(1)

        Set oAPI = CreateObject("MOM.ScriptAPI")
        Set oBag = oAPI.CreatePropertyBag()
        Call oBag.AddValue("ComputerName",sComputerName)
        Call oBag.AddValue("EventID",100)
        Call oBag.AddValue("ParamValue","Param1")

        oAPI.Return(oBag)

        ```

    4.  Click **Parameters**.

    5.  Select **Target**, select **\(Host\=Windows Computer\)**, and then select **Principal Name \(Windows Computer\)**.

    6.  Type a SPACE.

    7.  Select **Target** and then **Version \(My Computer Role Base\)**.

    8.  Click **OK**.

    9. Click **Next**.

9. On the **Event Mapper** page, do the following:

    1.  In the **Computer** box type **$Data\/Property\[@Name\='ComputerName'\]$**.

    2.  In the **Event source** box type **MyApp**.

    3.  In the **Event log** box type **CustomScript**.

    4.  In the **Event ID** box type **$Data\/Property\[@Name\='EventID'\]$**.

    5.  In the **Category** box type **0**.

    6.  In the **Level** box select **Information**.

    7.  Click the **Parameters** button.

    8.  Type **$Data\/Property\[@Name\='ParamValue'\]$**

    9. Click **OK**.

    10. Click **Create**.

## See Also
[Script Monitors and Rules](../Topic/Script-Monitors-and-Rules.md)

