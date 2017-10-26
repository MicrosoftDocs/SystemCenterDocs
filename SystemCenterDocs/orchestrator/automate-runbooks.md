---
title: Automate IT Operations with Runbooks
description: Provides an overview of runbook concepts and operations in System Center Orchestrator
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df19c898-2018-441e-a37d-62a38734318b
ms.author: raynew
ms.date: 03/21/2017
author: cfreemanwa
ms.manager: carmonm

---
# Automate IT Operations with System Center 2016 - Orchestrator Runbooks

> Applies To: System Center 2016 - Orchestrator

The power of System Center 2016 - Orchestrator lies in providing runbooks and the individual activities that make up a runbook. Runbooks contain the instructions for an automated task or process. The individual steps throughout a runbook are called activities. Within the runbook,  additional controls provide information and instructions to control the sequence of activities in the runbook. Runbooks, activities, and each runbook control have configurable properties. You modify these properties to configure the behavior that your runbook requires.  

## Starting Point
Your runbook must have only one starting point. A starting point is an activity that automatically runs when the runbook is started. Each activity in the runbook runs after the previous activity in the workflow is completed.  

If a runbook starts with any activity other than a monitor activity, the runbook begins processing and attempts to run to completion. If the runbook starts with a monitoring activity, the monitor loads and waits for the trigger condition. When the condition is met, a runbook instance is created to run the remaining activities in the runbook. The monitor continues to run and waits for another occurrence of the trigger condition. Runbooks that start with monitors continue to run until you stop them from the Runbook Designer or Orchestration console.

## Variables
When building runbooks some settings are the same across activities. Variables let you specify a value that activities use in any runbook.  

> [IMPORTANT]  
> The access permissions for variables can be modified, but the runbook server does not enforce these permissions.  

> [IMPORTANT]  
> Be aware that in Orchestrator, variables that reference system variables, for example **%ProgramFiles%**, return values from a 32-bit runtime environment. This is because Orchestrator is a 32-bit application.  

> [NOTE]  
> Orchestrator does not support moving multiple variables with multiple-selection. To move more than one variable to another folder, you must move each variable individually.  

Use the following procedures to create, insert, and organize variables.  

### To create a variable  

1.  In the **Connections** pane in the Runbook Designer, expand the **Global Settings** folder, and then click the **Variables** folder.  

2.  Right-click the **Variables** folder or a subfolder of the **Variables** folder to select **New**, and then click **Variable** to open the **New Variable** dialog box.  

3.  In the **Name** box, type a name for the variable.  

4.  In the **Description** box, type a description that explains the purpose of the variable.  

5.  In the **Value** box, type the value of the variable. This value replaces the placeholder in those activities where the variable is inserted.  

6.  If you want the variable to be encrypted \(for example, to store a password for use in other runbook activities\), select the **Encrypted Variable** check box.  

    For more information about best practices for using encrypted variables, see [Orchestrator Data Encryption](https://technet.microsoft.com/en-us/library/hh912316.aspx).  

7.  Click **Finish**.  

> [IMPORTANT]  
> System Center 2016 - Orchestrator does not let you combine an encrypted variable with plain text as a parameter value in a runbook.  

### To insert a variable in an activity  

1.  Right-click the applicable activity from your runbook to select **Properties**, and then click the **Details** tab to open the activities properties dialog box.  

2.  In a text box, to open a menu, right-click to select **Subscribe**, and then click **Variable** to open the **Select a Variable** dialog box.  

3.  Select the variable name, and then click **OK**.  

    A placeholder `{variable}` is inserted next to the computer name in the **Computer** box.  

    When the activity runs, the placeholder is replaced with the value of the variable.  

### To organize variables  

1.  You can group variables into folders to organize them. To create a folder, right-click the **Variables** folder to select **New**, and then click **Folder**.  

2.  To move a variable to a different folder, right-click the variable, and then click **Move** to open the **Select a Folder** dialog box.  

3.  Select the destination folder, and then click **OK**. The variable is moved to the new folder location.  

## Special Variables  
You can specify special formats of variables to provide dynamic information to your runbooks. Specify the value of the variable to invoke this behavior.  

**NOW\(\)**: When the variable is resolved, it is set to the current date and time. You can pass arguments to this function to return specific portions of the date or time. For example, NOW\(hour\) returns the current hour. The following are the valid arguments for the NOW\(\) function: day, dayofweek, dayofyear, month, year, hour, minute, second, millisecond.  

**%ENVVAR%**: This variable returns the value of the environment variable between the percent \(%\) symbols. The environment variable is based on the runbook server computer where the runbook is running, and it is not case\-sensitive. All system variables can be resolved. Any user variables are resolved in the context of the service account on the runbook server. If the environment variable does not exist, the text specified within the variable is returned as\-is \(that is, if you type %ENVVAR% and no environment variable named ENVVAR exists, the text '%ENVVAR%' is returned\).  

## Workflow Control
When you build runbooks in System Center 2016 - Orchestrator, it is important to understand the underlying logic of the workflow engine. By using this logic, you can create workflows to automate resource\-based jobs and complex data processing tasks.  

The workflow control provides the following controls: Smart Links and Embedded Loops.  

### Smart Links

The links that connect individual activities in a runbook are called smart links. Smart links in System Center 2016 - Orchestrator support precedence between two activities. Smart links invoke the next activity in the runbook as soon as the previous activity finishes successfully. Smart links also provide filtering capabilities for the data so you can limit the data passed to subsequent activities in the workflow.

### Embedded Loops   

Each activity can create a loop so that you can retry operations if they fail or test the output information of the activity for valid data. You can also use these mechanisms to build wait conditions into your workflows.  

When a loop is configured for an activity, it continues to run with the same input data until a desired exit looping criteria is reached. The exit criteria is built in a similar way as smart link configurations. You can use any published data item from the activity as part of the exit or do not exit configuration. Included in the common published data are special data items such as **Loop: Number of attempts** and **Loop: Total duration** that let you use information from the loop itself in the looping conditions.  

Loops run one time for each incoming piece of data that is passed to the activity. For example, consider a runbook that uses a **Query Database** activity followed by **Append Line**. If the **Query Database** activity returned three rows, the **Append Line** activity would run three times. If you have a loop on the **Append Line** activity, it would run three separate loops. After the first data item has looped through the **Append Line** activity, the next item goes through **Append Line** and loops until it exits, and then the third begins. After all three items have been processed, the next activity in the runbook runs.

## Extending Runbook capabilities 

System Center 2016 - Orchestrator provides two options for extending standard activities. You can either build new activities, or create new Integration Packs (IP). IPs are collections of activities for Microsoft and products of other companies  which are specific to a product or technology. If the functionality that you require is not available in an IP, you have the alternative option of using the Orchestrator Integration Toolkit. 

The System Center 2016 Orchestrator Integration Toolkit is a set of tools to help you create new integrations for Orchestrator. You can use wizards in the Integration Toolkit to easily create new workflow activities and Integration Packs that extend the capabilities of the product. You can also create custom workflow activities using the Orchestrator SDK and C\#, and then package them into an IP using this toolkit.

## Next steps

- Get detailed information about the Integration Tookit at: [System Center 2012 Orchestrator Integration Toolkit](https://go.microsoft.com/fwlink/?LinkId=261687)
- Learn more about how to design and build runbooks at: [Build and test runbooks for System Center 2016 - Orchestrator](build-test-runbooks.md).
