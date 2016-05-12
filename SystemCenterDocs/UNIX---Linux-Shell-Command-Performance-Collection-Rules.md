---
title: UNIX - Linux Shell Command Performance Collection Rules
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9c1f2f1-1b69-413d-a558-c1c45d9e34dd
---
# UNIX - Linux Shell Command Performance Collection Rules
To define a collection rule in Operations Manager based on the output of an UNIX\/Linux shell command, the command execution details, object name and counter name of the performance counter must be defined with a frequency that specifies how frequently to sample the data.

## UNIX\/Linux Shell Command Performance Collection Wizard Options
When you run the UNIX\/Linux shell command performance collection wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### Rule Type
The Rule Type page includes basic settings for the rule including its type and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Select the type of rule to create|To create a performance collection rule based on the execution of an UNIX\/Linux shell command, select **UNIX\/Linux Shell Command \(Performance\)**.|
|Management Pack|Management pack file to store the rule or monitor.For more information on management packs, see [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).|

### General
The **General** page includes general settings for the rule including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Rule Name|The name used for the rule. This appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it.|
|Description|Optional description of the rule.|
|Management Pack|Management pack to store the rule. For more information on management packs, see [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).|
|Rule Category|The category for the rule. For a performance collection rule, this should be **Performance Collection**.|
|Rule Target|The class to use for the target of the rule. The rule will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](Understanding-Classes-and-Objects.md).|
|Rule is Enabled|If checked, the rule is enabled and the shell command will run according to the schedule. If unchecked, the rule is not enabled and the script will not run. The rule can be enabled for a group of target objects by creating an override to enable the rule.|

### Schedule
The following options are available on the **Schedule** page of the wizard.

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

### Filter Expression
Shell commands used in performance collection rules must return only a single numeric value, or errors will be encountered when collecting the performance value. The **Filter Expression** page allows you to filter the command output to ensure that the command output is acceptable. It is recommended that the default expression filter is used to only collect performance data when the value is numeric and the command executed successfully.

|Property Name|Description|
|-----------------|---------------|
|Filter one or more events|An expression that filters output of the shell command. For more information on building expressions, see [Expressions](Expressions.md).<br />The Parameter Name syntax for command execution output is:<br />**StdOut**: \/\/\*\[local\-name\(\)\="StdOut"\]<br />**StdErr**: \/\/\*\[local\-name\(\)\="StdErr"\]<br />**Return Code**: \/\/\*\[local\-name\(\)\="ReturnCode"\]<br />The default expression filters that the StdOut value is numeric, and that the script executed successfully, with the expression definition of:<br />**\/\/\*\[local\-name\(\)\=”StdOut”\] Matches Regular Expression ^\[\-\+\]?\\d\*\[0\-9\]\*\(\\.\[0\-9\]\+\)?\[Ee\]?\[\-\+\]?\[0\-9\]\*$**<br />**\/\/\*\[local\-name\(\)\=”ReturnCode”\] Equals 0**|

### Performance Mapper
The **Performance Mapper** page defines the mapping of the command output to a performance counter.

|Option|Description|
|----------|---------------|
|Object|Text for the Object name. This is required. You can type in the name of the object or select a property from the target.|
|Counter|Name of the performance counter.|
|Instance|Text for the Instance name. This only required if the performance counter has multiple instances. You can type in the name of the instance or select a property from the target.|
|Value|The variable that defines the value collected as a performance counter value. To collect the value returned by the command as StdOut, use **$Data\/\/\/\*\[local\-name\(\)\=”StdOut”\]$**.  To collect the value returned by the command as ReturnCode, use **$Data\/\/\/\*\[local\-name\(\)\=”ReturnCode”\]$**|

## Creating UNIX\/Linux Shell Command Performance Collection Rules
Use the following procedures to create a Windows performance collection rule in Operations Manager with the following details:

-   Runs on all UNIX\/Linux Computers, every 15 minutes

-   Collects the count of files in the \/tmp path as a performance counter

#### To create an UNIX\/Linux shell command performance collection rule in Operations Manager

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

3.  Right\-click **Rules** and select **Create a new rule**.

4.  On the **Rule Type** page, do the following:

    1.  Expand **Collection Rules**, expand **Probe Based**, and then click **UNIX\/Linux Shell Command \(Performance\)**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Rule name** box, type **\/tmp File Count**.

    2.  In the **Rule Category** box, select **Performance Collection**.

    3.  Next to **Rule Target**, click **Select** and then select **UNIX\/Linux Computers**.

    4.  Leave **Rule is enabled** selected.

    5.  Click **Next**.

6.  On the **Schedule** page, do the following:

    1.  In the **Run Every** boxes, input **15** and **Minutes**.

    2.  Click **Next**.

7.  On the **Shell Command Details** page, do the following:

    1.  In the **Command** box, type **ls \/tmp | wc –l**. This command sequence will return the count of the files in \/tmp.

    2.  In the **Run As Profile** box, select the **UNIX\/Linux Action Account** profile.

    3.  In the **Timeout \(Seconds\)** box, input **120**.

    4.  Click **Next**.

8.  On the **Filter Expression** page, do the following:

    1.  Click **Next** \(to use the default expression filter that validates StdOut is a numeric value, and the command executed successfully\).

9. On the **Performance Mapper** page, do the following:

    1.  On the **Object** line, click **\[…\]**.

    2.  Click **Target** and select **Network Name**.

    3.  Click **OK**.

    4.  In the **Counter** box, type **File Count**.

    5.  In the **Instance** box, type **\/tmp**.

    6.  In the **Value** box, type **$Data\/\/\/\*\[local\-name\(\)\=’StdOut’\]$**

    7.  Click **Create**.

## See Also
[Performance Monitors and Rules](Performance-Monitors-and-Rules.md)
[Performance Monitors](Performance-Monitors.md)


