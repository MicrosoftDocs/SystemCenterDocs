---
title: UNIX-Linux Shell Command Alerts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcfac291-c215-4361-a217-15fb08176c87
author:markgalioto
---
# UNIX-Linux Shell Command Alerts
UNIX\/Linux shell commands can be used to detect events and generate alerts. When the rule is run, the provided command is executed on the agent, and if the output matches the provided filter, the alert is generated.  
  
## Target  
Rules and monitors run on the agent computer of each instance of the target class, and they usually access data on the local computer. The target must be a UNIX and Linux computer type, such as **UNIX\/Linux Computer**, **Linux Computer**, etc.  
  
## UNIX\/Linux Shell Command \(Alert\) Wizard Options  
When you run a UNIX\/Linux Shell Command rule wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.  
  
### Rule Type  
The Rule Type page includes basic settings for the rule including its type and the management pack file to store it in.  
  
|Option|Description|  
|----------|---------------|  
|Select the type of rule to create|To create an alert\-generating rule based on the execution of an UNIX\/Linux shell command, select **UNIX\/Linux Shell Command \(Alert\)**.|  
|Management Pack|Management pack file to store the rule or monitor.For more information on management packs, see [Selecting a Management Pack File](../../om/manage/Selecting-a-Management-Pack-File.md).|  
  
### General  
The General page includes general settings for the rule including its name, category, target, and the management pack file to store it in.  
  
|Option|Description|  
|----------|---------------|  
|Name|The name used for the rule. The name appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it.|  
|Description|Optional description of the rule.|  
|Rule Category|The category for the rule. For a performance collection rule, this should be **Performance Collection**. For an alerting rule, this should be **Alert**.|  
|Rule Target|The class to use for the target of the rule. For more information on targets, see [Understanding Classes and Objects](../../om/manage/Understanding-Classes-and-Objects.md).|  
|Rule is enabled|If checked, the rule is enabled and the shell command will run according to the schedule. If unchecked, the rule is not enabled and the script will not run. The rule can be enabled for a group of target objects by creating an override to enable the rule.|  
  
### Schedule  
The following options are available on the Schedule page of the wizard.  
  
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
The Filter Expression page allows you to filter for output to generate an alert. The alert is generated only if the output of the shell command matches the filter expression.  
  
|Property Name|Description|  
|-----------------|---------------|  
|Filter one or more events|An expression that filters output of the shell command. For more information on building expressions see [Expressions](../../om/manage/Expressions.md) The Parameter Name syntax for command execution output is:<br />**StdOut**: \/\/\*\[local\-name\(\)\="StdOut"\]**StdErr**: \/\/\*\[local\-name\(\)\="StdErr"\]**Return Code**: \/\/\*\[local\-name\(\)\="ReturnCode"\]|  
  
### Configure Alerts  
The Configure Alerts page is used to define alert properties for the rule. Its options are explained in [Alerts](../../om/manage/Alerts.md).  
  
## Creating UNIX\/Linux Shell Command \(Alert\) Rules  
The following procedure shows how to create an UNIX\/Linux shell command alerting rule in Operations Manager with the following details:  
  
1.  Runs on all UNIX\/Linux Computers every 15 minutes  
  
2.  Generates an alert if the file “\/tmp\/error” exists  
  
#### To create a UNIX\/Linux shell command alerting rule  
  
1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](../../om/manage/Selecting-a-Management-Pack-File.md).  
  
2.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.  
  
3.  Right\-click **Rules** and select **Create a new rule**.  
  
4.  On the **Rule Type** page, do the following:  
  
    1.  Expand **Alert Generating Rules**, expand **Event Based**, and then click **UNIX\/Linux Shell Command \(Alert\)**.  
  
    2.  Select the management pack from step 1.  
  
    3.  Click **Next**.  
  
5.  On the **General** page, do the following:  
  
    1.  In the **Rule Name** box, type **Alert on Error File Exists**.  
  
    2.  In the **Rule Category** box, select **Alert**.  
  
    3.  Next to **Rule Target** click **Select** and then select **UNIX\/Linux Computer**.  
  
    4.  Leave **Rule is enabled** selected.  
  
    5.  Click **Next**.  
  
6.  On the **Schedule** page, do the following:  
  
    1.  In the **Run Every** boxes, input **15** and **Minutes**.  
  
    2.  Click **Next**.  
  
7.  On the **Shell Command Details** page, do the following:  
  
    1.  In the **Command** box, type **ls \/tmp\/error | wc –l**. This command sequence will return a 1 if the file “\/tmp\/error” exists, and a 0 if it does not.  
  
    2.  In the **Run As Profile** box, select the **UNIX\/Linux Action Account** profile.  
  
    3.  In the **Timeout \(Seconds\)** box, input **120**.  
  
    4.  Click **Next**.  
  
8.  On the **Filter Expression** page, do the following:  
  
    1.  Configure an **And** expression with the entries:  
  
        1.  **\/\/\*\[local\-name\(\)\=”StdOut”\] equals 1**  
  
        2.  \/\/\*\[local\-name\(\)\=”ReturnCode”\] equals 0  
  
    2.  This will trigger an alert whenever the value of the shell command output is **1**, and the command executed successfully.  
  
9. On the **Configure Alerts** page, do the following:  
  
    1.  In the **Alert name** box, type **Error File Found**.  
  
    2.  In the **Alert description** box, type **The file \/tmp\/error was found on the computer:**  
  
    3.  Click the **\[…\]** button.  
  
    4.  Click **Target** and select **Network Name**.  
  
    5.  Click **OK**.  
  
    6.  Click **Create**.  
  
## See Also  
[Event Monitors and Rules](../../om/manage/Event-Monitors-and-Rules.md)  
[Alerts](../../om/manage/Alerts.md)  
  
