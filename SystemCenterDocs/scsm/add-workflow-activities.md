---
title: Add or remove workflow activities
description: You can add or remove Service Manager workflow activities in a workflow to automate processes.
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 32de708f-02f7-4021-882b-14ed140ebc89
---

# Add or remove Service Manager workflow activities

Workflow activities are the building blocks of a workflow. You can use the procedures in this section to add activities to a workflow; remove, copy, and paste activities; and configure specialized activities to import Windows PowerShell scripts into your workflow.  

## Add an activity to a workflow

Use this procedure to add an activity to a workflow from the **Activities Toolbox** pane in the Service Manager Authoring Tool.  

 In the Woodgrove Bank customization scenario, Ken uses this procedure to add the Windows Workflow Foundation \(WF\) activities **Add AD DS Computer to Group** and **Set Activity Status to Completed** to his workflow.  

To add an activity to a workflow, follow these steps:

1. In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow you want, and select **Edit**. This opens the workflow in the authoring pane. For example, right\-click **AddComputerToADGroupWF**, and select **Edit**.  

2. In the **Activities Toolbox** pane, locate the appropriate activity group.  

3. Drag the activity you want to the authoring pane, and then drop it between the workflow Start and End icons or between two existing activities. The sequence of activities that is displayed in the authoring pane—from the top down—represents the order in which the activities will run. To run activities in a loop or if-else structure, drag the structure activity (such as [For Each Loop](workflow-activity-ref.md)) onto the authoring pane first, and then drop the activities into the structure activity.  

     For example, drag **Add AD DS Computer to Group** from the **Active Directory Activities** group to the authoring pane, and then drop it between the workflow Start and End icons. Then, drag **Set Activity Status to Completed** and drop it between the previous activity and the End icon.  

4. You can set the properties of an activity immediately after you add it to the authoring pane, or you can set the properties later.  

    > [!NOTE]  
    > If you don't set the properties at this time, the activity might be marked with a Red Exclamation Point icon. This icon indicates that one or more properties of the activity must be set before the activity can run. To see a list of these required properties, select the icon.

## Copy and paste an activity within a workflow

If your workflow uses multiple activities of the same type \(such as multiple Add AD DS Computer To Group activities\), you can use copy and paste functionality in the Service Manager Authoring Tool to quickly duplicate activities. To duplicate the values of the activity's properties with the activity, set the values for the properties, and then copy and paste the activity.  

### Copy and paste an activity  

1. In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow you want, and select **Edit**. This opens the workflow in the authoring pane.  

2. In the authoring pane, right\-click the activity, and select **Copy**.  

3. Do one of the following:  

    - To paste the activity at the end of the workflow, right\-click the authoring pane, and select **Paste**.  

    - To paste the activity immediately after an existing activity, right\-click the existing activity, and select **Paste**.  

## Add a script to a workflow

The Activity Library includes specialized activities that incorporate Windows PowerShell scripts, VBScript scripts, or command\-line scripts into workflows. Use a script activity to import the content of the script and to define the parameters that the script requires to run. The Service Manager Authoring Tool creates a task in the management pack to manage the script and store the script content and parameters.  

 Service Manager doesn't verify the script parameters; therefore, you've to ensure that the script logic handles validation. Also, when you create an incident with an extended property and don't provide a value for the extended property, the value of the parameter isn't parsed, and it's passed as $Data\/Property.  

 Script activities run as a separate process from the workflows; however, they also run under the security context of the Service Manager Workflow account.  

 Use the following procedure to add a script to a workflow.  

To add a script to a workflow, follow these steps:

1. In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow that you want, and select **Edit**. This opens the workflow in the authoring pane.  

2. In the **Activities Toolbox** pane, locate the activity group **Script Activities** and its subgroup **Generic Script Activities**. Drag the script activity that you want to use to a position between the workflow start and workflow end icons or between two existing activities.  

3. Set the script activity properties:  

    1. In the **Details** pane, select any of the properties in the **Activity Inputs** category, and select the ellipsis button (**...**) that appears next to the property.  

    2. In the **Configure a Script Activity** dialog, select **Import Script**. In the **Import** dialog, select the script file that you want to use, and select **Open**.  

        > [!CAUTION]  
        > After you import a script for a script activity, if you select **Import Script** again, any new script that you import completely replaces the previous script.  

    3. Select **Script Properties**. To create a parameter for the script, select **New**, and in the **Name** column, enter a name.  

        > [!NOTE]  
        > For VBScript script and command script activity, there's no **Name** column.  

    4. To set a value for the parameter, in the **Value** column, enter a constant value. If appropriate for the parameter, enter switch characters such as '\/t', which is typical for command scripts.  

    5. To bind the parameter to another property so that the parameter obtains its value from that property, select the corresponding ellipsis button (**...**). In the **Bind 'Parameter' to Activity Property** dialog, select the property that you want to use.  

    6. If you're working with a script that requires Windows PowerShell snap\-ins in order to run, in the **Windows PowerShell snap\-ins** box, enter the names of the snap\-ins, separated by semicolons.  

    7. Select **OK** to close the **Configure a Script Activity** dialog.  

## Add a control flow activity to a workflow

Use control flow activities to provide structure—branches, loops, or timer delays—for your workflow. The Service Manager Authoring Tool provides four built\-in control flow activities:  

- [Delay Activity](workflow-activity-ref.md) - Introduces a delay between the activities in a workflow.  

- [For Each Loop Activity](workflow-activity-ref.md) - Takes as an input an array \(*collection*\) of objects, and repeats the set of activities in the **For Each Loop** object in the collection.  

- [IfElse Activity](workflow-activity-ref.md) - Controls the sequence of activities in a workflow based on a Boolean \(True\/False\) condition.  

- [Parallel Activity](workflow-activity-ref.md) - Forks the sequence of activities into two simultaneous sequences of activities.  

To use a **Delay** activity, just drag the **Delay** activity into the workflow, and then set the activity's **TimeoutDuration** property to the delay interval you want to use. To use an **IfElse** or **Parallel** activity, drag the activity into the workflow, and then drop regular activities into the **IfElse** or **Parallel** activity.  

Using a **For Each Loop** activity resembles using an **IfElse** or **Parallel** activity; however, you might want to set additional properties for the activities in the **For Each Loop**. Use the following procedure to add a **For Each Loop** to a workflow.  

### Add each loop to a workflow  

1. In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow you want, and select **Edit**. This opens the workflow in the authoring pane.  

2. In the **Activities Toolbox** pane, locate the activity group **Control Flow**.  

3. Drag the **For Each Loop** activity to a position between the Workflow Start and Workflow End icons or between two existing activities.  

4. Add the activities for which you want to loop the execution to the **Loop Container\(ForEachChildActivity\)**. To add each activity:  

    1. In the **Activities Toolbox** pane, expand the activity group that contains the activity that you want to use.  

    2. Drag the activity to a position to the top of the **Loop Container** activity. If the **Loop Container** activity already contains other activities, drag the new activity to a position before, after, or between the existing activities.  

    3. Most workflow activities that you place in this container have two additional properties: **Current Item** and **Property to Bind**. For each activity within the loop container, set these properties as follows:  

        > [!NOTE]  
        > Setting the properties isn't mandatory, and it's useful only if you want to take the object from the **Input Collection** of the **Loop Container**.  

        1. Set **Current Item** to the **Current Item** property of the **Loop Container** activity of the **ForEach** activity.
            > [!NOTE]
            > If this activity is the first activity in the **For Each Loop**, **Current Item** is set automatically.  

        2. Set the value of the **Property to Bind** property to the value of the property of the current activity that will use the **Current Item** value.  

## Remove an activity from a workflow

Use this procedure to remove an activity from a workflow in the Service Manager Authoring Tool. This operation doesn't remove the activity from the Activity Library or from the **Activities Toolbox** pane.  

To remove an activity from a workflow, do the following:

- In the authoring pane, right\-click the activity, and select **Delete**.  

## Next steps

- [Configure the way activities manage and pass information](configure-activities-information.md).
