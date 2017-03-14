---
title: Manage workflows
description: Describes how to manage workflows with the Service Manager Authoring Tool.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42812658-2d83-4cd1-b86f-bacd91add82d
---

# Manage workflows with the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

Use the procedures in this section to create or delete workflows in the Service Manager Authoring Tool. The Authoring Tool provides a wizard to help you create workflows.  

 All workflows run under the security context of the Service Manager Workflow account.  

## Create a new workflow

Use the Create Workflow Wizard to create a new workflow in the Service Manager Authoring Tool. After you create the workflow, you can populate the workflow with activities, as described in [Adding or Removing Workflow Activities](author-adding-or-removing-workflow-activities.md).  

> [!IMPORTANT]  
>  All workflows run under the security context of the Service Manager Workflow account.  

 The following procedures guide you through the process of creating a new workflow:  

-   If you want to create a workflow that runs according to a schedule or a fixed time interval, use the procedure "To create a new workflow triggered by a timer or schedule."  

-   If you want to create a workflow that runs in response to a change in the Service Manager database, use the procedure "To create a new workflow triggered by a database change." In the Woodgrove Bank customization scenario, Ken uses this procedure to create a workflow named **AddComputertoADGroupWF**.  

> [!IMPORTANT]  
>  After you have completed the wizard, you cannot change the type of trigger that the workflow uses. For example, after you create a workflow that uses a timer trigger, you cannot change it to use a database trigger instead.  

### To create a new workflow triggered by a timer or schedule  

1.  In the Authoring Tool, open the management pack where you want to store this workflow.  

2.  In the **Management Pack Explorer**, right\-click **Workflows**, and then click **Create**.  

3.  On the **General** page of the Create Workflow Wizard, enter a name for the workflow. The name must include only alphanumeric or underscore characters, have 50 or fewer characters, and start with an alphabetical or underscore character, and it cannot have spaces. For example, enter **AddComputerToADGroupWF**.  

4.  If you want to add a description of the workflow, type it in the **Description** box. Note that, although there is no limit on the length of this text, some views \(such as the list of the workflow's properties on the **Summary** page of the wizard\) might only display the first 200 characters.  

5.  If you want to change the default values for the workflow retry interval and the maximum time to run, on the **General** page, click **Advanced**. In the **Advanced** dialog box, set new values for **Interval** and for **Maximum time to run the workflow**, and then click **OK**. Note that the value for the maximum time to run must be more than 60 seconds, but less than 24 hours.  

6.  On the **Trigger Condition** page, if you want the trigger to run at a specific time or at a specific interval, use the default setting **Timer**, and then click **Next**.  

7.  On the **Trigger Criteria** page, configure the interval at which to run the workflow \(either **Weekly** or **Other Interval**\):  

    1.  To set the workflow to run on specific days of the week, click **Weekly**. Use the **Start time** dial control to set a start time for the rule. To set the hour, minutes, or 00:00\-24:00 values, click the value, and then click the up arrow or down arrow. Then, select the check boxes for each day that you want the rule to run.  

        > [!NOTE]  
        >  The time that you set is the time on the Service Manager server that runs the workflow, not the local time on the server that runs the Authoring Tool.  

         \-or\-  

         To set the workflow to repeat after a specific time, click **Other Interval**. In the **Frequency** box, enter an integer value, and then select the type of interval \(**Days**, **Hours**, **Minutes**, or **Seconds**\).  

    2.  After you have set the interval for the workflow, click **Next**.  

8.  On the **Summary** page, review the settings for the new workflow, and then click **Create**. After the wizard is completed, click **Close**.  

### To create a new workflow triggered by a database change  

1.  In the Authoring Tool, open the management pack where you want to store this workflow.  

2.  In the **Management Pack Explorer**, right\-click **Workflows**, and then click **Create**.  

3.  On the **General** page of the **Create Workflow** wizard, enter a name for the workflow. The name must include only alphanumeric or underscore characters, have 50 or fewer characters, and start with an alphabetical or underscore character, and it cannot have spaces. For example, enter **AddComputerToADGroupWF**.  

4.  If you want to add a description of the workflow, type it in the **Description** box. Note that, although there is no limit on the length of this text, some views \(such as the list of the workflow's properties on the **Summary** page of the wizard\) might only display the first 200 characters.  

5.  If you want to change the default values for the workflow retry interval and the maximum time to run, on the **General** page, click **Advanced**. In the **Advanced Workflow Limits** dialog box, set new values for these options, and then click **OK**. Note that the value for the maximum time to run must be more than 60 seconds, but less than 24 hours.  

6.  On the **Trigger Condition** page, click **Run only when a database object meets specified conditions**, and then click **Next**.  

7.  On the **Trigger Criteria** page, to select a **Class name**, click **Browse**. In the **Class Property** dialog box, select the class of object with which the workflow will interact, and then click **OK**. For example, select **Automated Activity: Add Computer To AD Group**.  

8.  To select a **Change event**, click the drop\-down list, select one of the options, and then click **Next**. For example, click the drop\-down list, and then click **When an instance of the class is updated**.  

9. Optionally, under **Add Criteria to this trigger**, click **Additional Criteria** to set advanced criteria, such as when the activity status changes from **Pending** to **In Progress**.  

10. On the **Summary** page, review the settings for the new workflow, and then click **Create**. After the wizard is completed, click **Close**.  

## Save and build a workflow

Workflows are saved whenever you save the management pack. In addition, when you save a management pack, the Service Manager Authoring Tool automatically identifies the Windows Workflow Foundation \(WF\) workflow files that are associated with the workflow information in the management pack and builds them into workflow assemblies. \(Each WF workflow may have multiple raw files.\) The tool builds one assembly per workflow.  

### To save and build workflows  

-   In the **Management Pack Explorer**, right\-click the management pack, and then click **Save**.  

## Copy a workflow
Use this procedure to create a copy of a workflow in the Service Manager Authoring Tool. After you copy the workflow, you can edit the properties of either the copy or the original.  

### To copy a workflow  

-   In the **Management Pack Explorer**, expand **Workflow**, right\-click the workflow you want to copy, and then click **Copy**.  

     The Authoring Tool creates a copy of the workflow and gives it a name that consists of the original workflow name and "\_Copy."  

## Edit a workflow's details

Use this procedure to edit workflow details in the Service Manager Authoring Tool.  

### To edit workflow details  

1.  In the **Management Pack Explorer**, expand **Workflow**, right\-click the workflow, and then click **Details**. If you are already editing the workflow, right\-click the authoring pane background, and then click **Details**.  

2.  If you want to edit the workflow description, in the **Details** pane, click the **Description** box and type a new description, or click the ellipsis \(**...**\) button to open the **Workflow Properties** dialog box. Click the **Description** box, and then edit the description.  

3.  If you want to edit any of the other workflow details, in the **Details** pane, click any of the details, and then click the ellipsis \(**...**\) button to open the **Workflow Properties** dialog box. You can edit the following details:  

    -   **Name**: On the **General** tab, click **Name**, and then edit the workflow name.  

    -   **Retry and timeout limits**: On the **General** tab, click **Advanced**, and then edit the appropriate values.  

    -   **Trigger condition for a timer\-based workflow**: On the **Scheduler** tab, edit the appropriate values.  

    -   **Trigger condition for a query\-based workflow**: On the **Trigger** tab, edit the appropriate values.  

        > [!IMPORTANT]  
        >  If you change the trigger class of the workflow while the workflow is open in the authoring pane, any activity details that were set to use values from properties of the trigger class are cleared. The workflow does not run until you reset those activity details to use values from the new trigger class.  

    > [!IMPORTANT]  
    >  You cannot change the type of trigger that the workflow uses. For example, after you create a workflow that uses a timer trigger, you cannot change it to use a query trigger instead.  

## Delete a workflow

Use this procedure to delete a workflow in the Service Manager Authoring Tool.  

### To delete a workflow  

1.  In the **Management Pack Explorer**, expand **Workflow**, right\-click the workflow you want to delete, and then click **Delete**.  

2.  To make sure that the workflow is permanently deleted, save the management pack.  
