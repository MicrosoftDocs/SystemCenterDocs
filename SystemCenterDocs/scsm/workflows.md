---
title: Configure Workflows
description: Learn about configuring workflows in Service Manager.
ms.topic: how-to
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.service: system-center
keywords:
ms.date: 05/27/2025
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.assetid: b204c2fc-c65e-41f3-a650-e425060f61b3
ms.custom: UpdateFrequency3, engagement-fy24
---

# Configure workflows in Service Manager

In Service Manager, a workflow is a sequence of activities that automate a business process. Workflows can, for example, update incidents when various changes occur. A workflow can automatically generate incidents when computers fall out of compliance from desired configuration management. You create a workflow that defines when and under what circumstances it will run. For example, a workflow can automatically change the support tier from a setting of 1 to 2 whenever a low-priority incident pertaining to printing problems is changed to a higher priority. Workflow activities function by the application of templates. For this example, an incident template to change the support tier to a setting of 2 must have been created previously.

In this article, you'll learn about configuring workflows in Service Manager.

You can create multiple workflows for each workflow configuration. You can enable or disable the workflow conditions. If a particular rule is disabled, the remaining rules still cause the workflow to run. If you want to completely disable a workflow, you must disable all of the rules that call the workflow.

The success or failure of a workflow is retained by Service Manager, and it's available for you to view. Two views are available. **All Results** consists of a view of all success and failure instances, and the **Errors** view displays only those instances when a workflow failed. In the **All Results** view, you can, for each instance, view the log and view the related object. When you view the log, you can examine the events that occurred when the workflow ran. When you view the related object, you see the form that this workflow acted on. The **Errors** view is limited to the most recent 250 instances. When you're viewing a failed instance, you've the same options in the **Success** view to view the log and view the related object. In addition, in the **Errors** view, you've the option to select **Retry** or **Ignore**. Selecting **Retry** causes the workflow to run again with the same parameters and removes this instance from the view. Selecting **Ignore** removes the instance from the view.

## Configure incident workflows

You can use the following procedure to create and configure a workflow rule that will change the support tier to **Tier 2** whenever the **Urgency** property of an incident that is related to printing problems is changed to **High**. This procedure assumes that you already created an incident template to change the support tier to **Tier 2**, and it assumes that you already created the priority calculation table. For more information, see [Set Incident Priority](./incident-mgt.md). To create a new printer-related incident template, see [Create Incident Templates](./incident-mgt.md).

To configure an incident workflow, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Workflows**, and select **Configuration**.
3. In the **Configuration** pane, double-click **Incident Event Workflow Configuration**.
4. In the **Configure Incident Event Workflows** dialog, select **Add**.
5. In the **Add Incident Event Workflow** dialog, complete these steps:
    1. On the **Before You Begin** page, select **Next**.
    2. On the **Workflow Information** page, in the **Name** box, enter a name for the workflow. For example, enter **Escalates Printer Problems to Support Tier 2 when the Urgency property is changed to High**.
    3. In the **Check for events** list, select **when an object is created or when an object is updated**, ensure that the **Enabled** checkbox is selected, and select **Next**.
    4. On the **Specify Event Criteria** page, select the **Changed to** tab. In the **Available Properties** list, select **Urgency**, and select **Add**. In the **Criteria** box, select **equals**. In the list, select **High**. Then, select **Next**.
    5. On the **Select Incident Template** page, select **Apply the following template**, and then select the template you created earlier that will set the support group to **Tier 2**. For example, select **Escalate Printer Problems to Tier 2**, and select **Next**.
    6. Optionally, in the **Select People to Notify** page, select the **Enable notification** checkbox, select the user to notify, and select **Next**.
    7. On the **Summary** page, review your settings, and select **Create**.
    8. On the **Completion** page, select **Close**.
6. In the **Configure Incident Event Workflows** dialog, select **OK**.

### Validate an incident workflow

To validate an incident workflow, follow these steps:

1. In the Service Manager console, select **Work Items**.
2. In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and select **All Incidents**.
3. In the **All Incidents** pane, double-click an incident that isn't currently assigned to the tier 2 support group.
4. In the **Incident Form** page, set the **Urgency** property to **High**, and select **OK**.
5. In a few minutes, press F5. Verify that the value in the **Support Group** box changed to **Tier 2**.

![Screenshot of PowerShell symbol.](./media/workflows/pssymbol.png) You can use Windows PowerShell commands to complete these and other related tasks, as follows:

- For information about how to use Windows PowerShell to create a new workflow in Service Manager, see [New-SCSMWorkflow](/previous-versions/system-center/powershell/system-center-2012-r2/hh316243(v=sc.20)).
- For information about how to use Windows PowerShell to retrieve configuration and status information for Service Manager workflows, see [Get-SCSMWorkflowStatus](/previous-versions/system-center/powershell/system-center-2012-r2/hh316207(v=sc.20)).
- For information about how to use Windows PowerShell to update workflow properties, see [Update-SCSMWorkflow cmdlet](/previous-versions/system-center/powershell/system-center-2012-r2/hh316204(v=sc.20)).
- For information about how to use Windows PowerShell to remove a workflow from Service Manager, see [Remove-SCSMWorkflow](/previous-versions/system-center/powershell/system-center-2012-r2/hh316221(v=sc.20)).

## View workflow success or failure in Service Manager

Use the following procedure to view the success or failure instances of the workflows.

To view workflow success or failure, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Workflows**, and select **Status**.
3. In the **Status** pane, select the workflow that you want to view. For example, select **Escalates Printer Problems to Support Tier 2 when the Urgency property is changed to High**.
4. In the **Status** results pane, select **Need attention** to view workflows that didn't run successfully. Or select **All Instances**, and then do the following:
    1. Select **View log** to view the list of events that occurred when the workflow ran.
    2. Select **View related object** to view the form that was used when the workflow ran.
    The status of each workflow is displayed in the **Status** column.

![Screenshot of the PowerShell symbol.](./media/workflows/pssymbol.png) You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to retrieve the status of workflows in Service Manager, see [Get-SCSMWorkflowStatus](/previous-versions/system-center/powershell/system-center-2012-r2/hh316207(v=sc.20)).

## Next steps

[Configure change and activity management](change-activity-mgt.md).
