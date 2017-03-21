---
title: Manage changes and activities
description: Provides an example scenario and details about how to managing changes and activities in Service Manager.
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
ms.assetid: 6228f358-1256-475f-8d63-9bdf62070ecd
---

# Manage changes and activities in Service Manager

>Applies To: System Center 2016 - Service Manager

Information Technology (IT) departments must manage changes to their IT environment and the risk associated with such changes. The change management features in Service Manager help you manage change by providing repeatable, predictable, and measured processes to implement change.

The sections in this article are organized according to common change management scenarios. Even though the sample scenarios refer to a fictitious organization, Woodgrove Bank, the scenarios and steps are based on real use, and they describe how to use the change and activity management features in Service Manager.

This sample scenario for System Center 2016 - Service Manager helps you achieve your goal of managing changes and activities by using multiple scenarios end to end. You can think of this sample scenario as a case study that helps put the individual scenarios and procedures in context.  

## Initiate classify change requests  
In the scenario that encompasses initiating and classifying a change request, Julia, the messaging support analyst, wants to propose and track a change. To do this, she creates a change request to capture information that she and others will use to evaluate, plan, develop, test, deploy, and assess changes. Julia starts by initiating the change request and then identifying its priority and category.  

In incident management scenarios, Phil created an incident in which a user had a messaging problem, and he completed an initial investigation of the problem. In this scenario, Julia continues to investigate the same incident. She verifies that the cause is a known issue with Microsoft Exchange Server and fixes it. She also determines that all Exchange servers need a update, not just a single server. Next, Julia views the service map for the Exchange service configuration item that requires the update, and she opens a change request from the service's configuration item form. Lastly, Julia attaches a saved screen shot to the change request, which might help later with the change request review.  

 After the change request is created, the change reviewers at Woodgrove Bank must approve the change request, and the change implementers must complete the actions that are required for the change. These review and implementation steps are defined in the change request as a set of review activities and manual activities.  

## Approve change requests  

In the scenario that encompasses approving a change request, Garret wants to enforce the Woodgrove Bank business process of requiring approval of any IT infrastructure changes before the changes are deployed. He wants to enforce this business process by using Service Manager to associate review activities for a change request. By requiring approval, the change request is implemented only after decision makers at Woodgrove Bank agree that the change is necessary. Garret can set up various review methods, such as unanimous voting, percentage of positive votes, or automatic approval.  

The procedures that are related to this scenario describe a change to Woodgrove Bank's IT infrastructure that is approved before deployment.  

## Suspend and resume change requests  

During the course of reviewing the readiness of a change request, Garret occasionally wants to put a change request on hold and then later resume that change request. For example, Julia previously created a change request. That change request depends on the additional work of an external team. Garret wants to put that change request on hold until the external team completes its work. Garret will resume the change request after the external team's work is complete. Garret also wants to occasionally unblock failed change requests.  

## Implement and close change requests  

After changes to Garret's IT infrastructure are tested and approved for deployment, his final step is to finish any remaining manual activities that are associated with the change request. A manual activity must be designated as either completed or failed. When all manual activities are completed, the change request is automatically set as completed, and it appears in the **Change Requests: Completed** view. If a manual activity fails, the change request is automatically set as failed, and it appears in the **Change Requests: Failed** view. When the change request appears in either view, Garret can close the change request. After a change request has been closed, it cannot be reopened.  

In the scenario that encompasses implementing and closing change requests, Aaron completes a warranty review manual activity. Next, Garret sets the change request's remaining manual activities to **Completed**, and closes the change request. Garret opens a second existing change request, sets the post\-implementation manual activity to **Failed**, and then closes that change request.  

## Initiate and classify a change request in Service Manager

The procedures in this section describe how to initiate and classify a change request in Service Manager from start to finish.  

A change request normally results in a change to a configuration item. Therefore, it is important to understand the difference between a related item and a linked or affected item. A related item indicates that an association exists between the change request and a configuration item or other change requests. In other words, the change request might affect the related item or it might not. An affected or linked item indicates that the change request is tied directly to the item and that the change will affect the item itself.  

Complete the following steps to initiate and classify a change request.  

### Create a new change request

You can use the following procedures in Service Manager to create a change request for servers that are part of a service and then validate the creation of the change request. First, you view items from the service dependency view. Then, you navigate to the configuration items and open a change request template. Lastly, you assess the priority, impact, and risk level of the request. Although you create the change request from a service dependency view, you can also create a new change request from other places in Service Manager.  

> [!NOTE]  
>  IDs that are assigned to change requests and incidents are not created in sequence. However, newer change requests and incidents are assigned IDs with a higher number than ones created previously.  

#### To create a change request  

1.  In the Service Manager console, click **Configuration Items**.  
2.  In the **Configuration Items** pane, expand **Business Services**, and then click **All Business Services**.  
3.  In the **All Business Services** pane, double\-click the service. For example, double\-click **IT Messaging Service**.  
4.  In the dialog box that opens, click the **Service Dependents** tab.  
5.  In the **Expand to** list, click **Level 1**, and then view the items in the list. Notice the server names. For example, **Exchange01.woodgrove.com** and **Exchange02.woodgrove.com** appear in the list.  
6.  In the **Service Dependents** list, select a computer, and then click **Open**. For example, select and open **Exchange01.woodgrove.com**.  
7.  In the computer form, click **Create Related Change Request** under **Tasks**.  
8.  In the **Select Template** dialog box, click a template, and then click **OK**. For example, click **Changes to messaging infrastructure template**.  
9. In the **Title** box, type a name for the change request. For example, type **Apply Exchange Server Service Pack**. Notice that various values in the form are populated with information from the change request template.  
10. In the **Description** and **Reason** fields, type a description and the reason for the change request. For example, type **Apply Exchange Server Service Pack to these servers** in the **Description** field, and type **The service pack fixes the problem that these servers have** in the **Reason** field.  
11. In the **Assigned To** field, enter the name of the person to whom you want to assign the change request. For example, type **Aaron Lee**.  
12. Specify the priority, impact, and risk. For example, In the **Priority** list, select **Medium**. In the **Impact** list, select **Standard**. In the **Risk** list, click **Medium**.  
13. In the **Config Items To Change** list, make sure that one server is listed, and then click **Add**.  
14. In the **Select Objects** dialog box, select another item to add to the change request, and then click **Add**. For example, select **Exchange02.woodgrove.com**, and then click **OK**.  
15. Click **OK** to close the change request form.  

#### To validate the creation of a change request  

1.  Open the service that contains the items for which you created the change request, and then click the **Service Dependents** tab.  
2.  In the **Service Components** list, notice that the two servers you opened the change request for are marked with **YES** under the **Affected By Change** column.  
3.  Click **Cancel** to close the service.  

### Add related items to a change request

You can use the following procedures to add related items to a change request and then validate the addition of the items. You can add related items, such as configuration items, incidents, other change requests, files, and knowledge articles. When you add files, such as saved screen shots, saved written procedures, and knowledge articles, reviewers and implementers can more easily review, approve, and implement the change.  

To add files to any work item, including change requests, you must first enable the appropriate option. For more information, see [How to Configure General Change Settings](admin-how-to-configure-general-change-settings.md).  

#### To add related items to a change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  
3.  In the **All Change Requests** pane, double\-click the change request to which you want to add an item.  
4.  Click the **Related Items** tab.  
5.  On the **Related Items** tab under **Attached Files**, click **Add** to attach a file to the change request.  
    > [!NOTE]  
    >  You might need to maximize the form to view buttons on the tab.  

6.  Under **Knowledge Articles**, click **Add** to attach a knowledge article to the change request.  
7.  Click **OK**.  

#### To validate that you added related items to a change request  

-   To verify that the file and knowledge articles were attached to the change request, reopen the change request, and then click the **Related Items** tab.

### Add manual activities to a change request

You can use the following procedures to add a manual activity and then assign it to yourself and then validate that the manual activity was added. For example, when you investigate a new change request, you might want to add a manual activity to the change request. This manual activity could be any task that is not defined in the change request template that was used to create the change request.  

> [!NOTE]  
>  You cannot delete an activity in a change request if the change request is in progress, however you can skip the activity or put the change request on hold and then delete the activity.  

#### To add a manual activity  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  
3.  Double\-click the change request to which you want to add a manual activity. For example, double\-click **Apply Exchange Server Update**.  
4.  Click the **Activities** tab, and then click **Add**. In the **Select Template** dialog box, click **Default Manual Activity**, and then click **OK**.  
5.  In the **Title** box, type a name that describes the manual activity. For example, type **Warranty Review**.  
6.  In the **Description** box, type a description of the manual activity. For example, type **Verify that the server is still under warranty before approval**.  
7.  Under **Activity Implementer**, click the ellipsis button \(...\).  
8.  In the **Select User** dialog box, select the name of the person who will perform the manual activity, and then click **OK**. For example, select **Aaron Lee**.  
9. Click **OK** to update the changes to the manual activity.  
10. Click **OK** to update the change request and to close the form.  

#### To validate that the manual activity was added  

-   Reopen the change request, and then click the **Activities** tab to view the manual activity that you added.  

### Add dependent activities to a change request for release records

You can use the following procedures to add a dependent activity to an existing change request, which is used as part of the release management process. Although you can add dependent activities to work items, such as release records and service requests, the primary purpose of a dependent activity is for use as a mechanism to associate a change request with a release record. Specifically, a manual activity in a release record is linked to the dependent activity in a change request. When it is completed, the dependent activity indicates that the release management process is complete for the change request.  

If you intend to use release management as part of the standard processes in your organization, consider adding dependent activities to change request templates. For more information about creating change request templates, see [How to Create Change Request Templates](admin-how-to-create-change-request-templates.md).  

#### To add a dependent activity to a change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  
3.  Double\-click the change request to which you want to add a dependent activity. For example, double\-click **Apply Exchange Server Update**.  
4.  Click the **Activities** tab, and then click **Add**. In the **Select Template** dialog box, click **Default Dependent Activity**, and then click **OK**.  
5.  In the **Title** box, type a name that describes the dependent activity. For example, type **Exchange Server Update - Deploy, Test, and Verify** .  
6.  In the **Description** box, type a description of the dependent activity. For example, type **Verify that the service pack is deployed, tested, and verified successful**.  
7.  Under **Owner**, click the ellipsis button \(...\).  
8.  In the **Select User** dialog box, select the name of the person who has overall responsibility for the dependent activity, and then click **OK**.  
9. Under **Assigned To**, click the ellipsis button \(...\).  
10. In the **Select User** dialog box, select the name of the person who will perform the dependent activity, and then click **OK**. For example, select **Aaron Lee**.  
11. As an option, specify scheduling information on the **Scheduling** tab.  
12. Click **OK** to update the changes to the dependent activity.  
13. Click **OK** to update the change request and to close the form.  

#### To validate that the dependent activity was added  

-   Reopen the change request, and then click the **Activities** tab to view the dependent activity that you added.  

## Approve and modify change requests

The procedures in this section describe how to approve a change request in Service Manager. Complete the following steps to approve or modify a change request.  

### Edit a change request

You can use the following procedures to edit a change request and then validate the edit. For example, you might want to change the priority of an existing change request from medium to high.  

> [!NOTE]  
>  You cannot delete an activity in a change request if the change request is in progress, however you can skip the activity or put the change request on hold and then delete the activity.  

#### To edit a change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  
3.  Double\-click a change request. For example, double\-click **Apply Exchange Server Service Pack**.  
4.  Make the change that you want. For example, if you want to change the priority to high, select **High** in the **Priority** list. Or, type new text in the **Description** box.  
5.  Click **OK** to update the change request and to close it.  

#### To validate an edited change request  

1.  Double\-click the change request that you updated.  
2.  Verify that your changes are displayed in the change request form.   

### Add a change reviewer

You can use the following procedures to add a change reviewer for an existing change request and then validate that the reviewer was added. You can select who reviews change requests in a way that supports your business processes. For example, if a change affects a process for which certain people are responsible, you can give those people the ability to approve change requests that affect the process.  

#### To add a change reviewer  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, click **Change Management**, and then click **All Change Requests**.  
3.  Double\-click a change request to open it. For example, double\-click **Apply Exchange Server Service Pack**.  
4.  Click the **Activities** tab to view the list of manual and review activities.  
5.  Double\-click the activity to which you want to add a reviewer. The activity must have a status of **In Progress** or **Pending**, and in the ID column, the activity must also have the **RA** prefix or the prefix you defined for review activities.  
6.  In the dialog box that appears, click **Add**, type the name of a reviewer, select **Must Vote**, and then click **OK**. For example, type **Aaron Lee**.  
7.  Click **OK** to close the dialog box, and then click **OK** to update the change request and to close the form.  

#### To validate that a reviewer was added  

1.  Double\-click the change request to which you added a reviewer. For example, double\-click **Apply Exchange Server Service Pack**.  
2.  Click the **Activities** tab, and then double\-click the activity to which you added a reviewer.  
3.  Verify that the reviewer was added.

### Approve a review activity using the console

You can use the following procedures to approve a review activity in the Service Manager console and then validate the approval. In many cases, multiple people or groups must vote to approve a single review activity before its approval is final.  

> [!NOTE]  
>  Users can only approve or reject the activities that are assigned to them.  

#### To approve a review activity for a change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Review Activities**, and then click **In\-Progress Activities**.  
3.  Select a review activity. For example, select the **Messaging Infrastructure Request Approval**.  
4.  In the **Tasks** pane, click **Approve**.  
5.  In the **Comments** dialog box, type any comments that you have for the approval or rejection, and then click **OK**.  

#### To validate review activity approval  

-   If all the reviewers approved the activity, the activity does not appear in the **In\-Progress Activities** view.  
-   If an activity is still in progress, it requires approval from other reviewers. Click **In\-Progress Activities**, and then open the activity to view your voting status.

### Send automated activity and change request notifications

You can use the following procedure to notify reviewers that an activity is available for review. You can use the second procedure to notify users that a change request has been closed.  

> [!NOTE]  
>  Only administrators can configure workflow notifications.  

#### To notify reviewers that an activity is available for review  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Workflows**, and then click **Configuration**.  
3.  Select **Activity Event Workflow Configuration**, and then click **Configure Workflow Rules** in the **Tasks** pane.  
4.  In the **Select a Class** dialog box, select **Review Activity**, and then click **OK**.  
5.  In the **Configure Workflows** dialog box, click **Add**.  
6.  In the Configure Workflows for Objects of Class Review Activity Wizard, click **Next** on the **Before You Begin** page.  
7.  On the **Workflow Information** page, type a name and a description for the workflow. In the **Check for events** list, ensure that the **When an object is updated** item is selected, and then click **Next**.  
8.  On the **Specify Criteria** page, select the **Changed From** tab. Under **Available Properties**, select **Status**, and then click **Add**.  
9. Under **Criteria**, select **Pending**, and then select the **Changed To** tab. Under **Available Properties**, select **Status**, and then click **Add**.  
10. Under **Criteria**, select **In Progress**, and then click **Next**.  
11. On the **Apply Template** page, clear the **Apply the selected template** check box, and then click **Next**.  
12. On the **Select People to Notify** page, select the **Enable notification**.  
13. Under **User**, select **Assigned To User**.  
14. Under **E\-mail Template**, if you cannot select a template, click **Create E\-Mail Template**. Otherwise, select an email notification template to apply.  
15. If you are creating an email notification template, complete the Create E\-Mail Notification Template Wizard.  
16. After you have selected an email template, click **Add**, ensure that **Reviewers** appears under the **User** column, and then click **Next**.  
17. On the **Summary** page, review the summary information, and then click **Create**.  
18. On the **Completion** page, click **Close**.  

#### To notify users that a change request has been closed  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Workflows**, and then click **Configuration**.  
3.  Select **Change Request Event Workflow Configuration**, and then click **Configure Workflow Rules** in the **Tasks** pane.  
4.  In the **Configure Workflows** dialog box, click **Add**.  
5.  In the Configure Workflows for Objects of Class Change Request Wizard, click **Next** on the **Before You Begin** page.  
6.  On the **Workflow Information** page, type a name and a description for the workflow. In the **Check for events** list, ensure that the **When an object is updated** item is selected, and then click **Next**.  
7.  On the **Specify Criteria** page, select the **Changed From** tab. Under **Available Properties**, select **Status**, and then click **Add**.  
8.  Under **Criteria**, select **Completed**.  
9. Click the **Changed To** tab.  
10. Under **Available Properties**, select **Status**, and then click **Add**.  
11. Under **Criteria**, select **Closed**, and then click **Next**.  
12. On the **Apply Template** page, clear the **Apply the selected template** check box, and then click **Next**.  
13. On the **Select People to Notify** page, select the **Enable notification** check box.  
14. Under **User**, select **Assigned To User**. Under **Template**, select **Assigned To User Notification Template**, click **Add**, and then click **Next**.  
15. On the **Summary** page, review the summary information, and then click **Create**.  
16. On the **Completion** page, click **Close**.  

#### To validate receipt of the notification  

-   The reviewer of the review activity or the user that the change request is assigned to receives an email message that indicates that a new review activity requires approval or that the change request was closed.

## Suspend and resume a Service Manager change request

The procedures in this section describe how to suspend and resume a change request in Service Manager. Complete the following steps to suspend or resume a change request.  


### Put a change request on hold

You can use the following procedures to put a change request on hold in Service Manager and then validate that the change request is on hold. For example, you might need to put a change request on hold if an external team needs to complete a manual activity.  

#### To put a change request on hold  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Manual Activity In Progress**.  
3.  Select a change request to put on hold. For example, select **Apply Exchange Server Service Pack**.  
4.  In the **Tasks** pane, click **Put On Hold**.  
5.  In the **Comments** dialog box, type a note that indicates why the change request was put on hold, and then click **OK**.  

#### To validate that the change request is on hold  

-   Click the **Change Requests: On Hold** view to ensure that the change request has been put on hold.  

### Resume a change request

You can use the following procedures to resume a change request that was put on hold in Service Manager and then validate that the change request was resumed. For example, you might need to resume a change request after an external team has completed a manual activity.  

#### To resume a change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: On Hold**.  
3.  Select a change request. For example, select **Apply Exchange Server Updates**.  
4.  In the **Tasks** pane, click **Resume**.  
5.  In the **Comments** dialog box, type a comment, and then click **OK**.  

#### To validate the change request was resumed  

-   If the current activity for a change request is a review activity, click the **Change Requests: In Review** view to ensure that the change request was resumed.  
-   If the current activity for a change request is a manual activity, click the **Change Requests: Manual Activity In Progress** view to ensure that the change request was resumed.  

### Optionally unblock a failed change request

You can use the following procedures to unblock a failed change request and then validate that the change request is unblocked. For example, you might need to unblock an activity of a change request that a review board or other review body has failed. Unblocking the change request resets the change request so that the change owner can provide more information.  

#### To unblock a failed change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Failed**.  
3.  Select a change request. For example, select **Apply Exchange Server Service Pack**.  
4.  In the **Tasks** pane, click **Return To Activity**.  
5.  In the **Return to Activity** dialog box, select the failed activity, type a comment in the **Comments** box, and then click **OK**.  

#### To validate the change request is unblocked  

-   If the failed activity for a change request is a review activity, click the **Change Requests: In Review** view to ensure that the change request is unblocked.  
-   If the failed activity for a change request is a manual activity, click the **Change Requests: Manual Activity In Progress** view to ensure that the change request is unblocked.  

## Implement and close a change request in Service Manager

The procedures in this section describe how to implement and close a change request in Service Manager.  

 Complete the following steps to implement and close a change request.  

### Complete or fail a manual Activity

You can use the following procedures to complete or fail a manual activity in Service Manager and then validate that the manual activity is complete or failed.  

#### To successfully complete a manual activity  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and then click **In\-Progress Activities**.  
3.  Select the manual activity.  
4.  In the **Tasks** pane, click **Mark as Completed**.  
5.  In the **Comments** box, type a comment, and then click **OK**.  

#### To fail a manual activity  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and then click **In\-Progress Activities**.  
3.  Select the manual activity.  
4.  In the **Tasks** pane, click **Mark as Failed**.  
5.  In the **Comments** box, type a comment, and then click **OK**. For example, type **The post\-implementation analysis indicates that the new hardware does not adequately meet our needs and has failed the review**.  

#### To validate that a manual activity is complete or failed  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and then click **All Activities**.  
3.  Verify that the manual activity is set to either **Completed** or **Failed**.  

### Close a change request

You can use the following procedures to permanently close a successful change request or a failed change request and then validate the closure of the change request. You cannot reopen a closed change request.  

> [!NOTE]  
>  If an end user cancels a software request before the software is deployed to the end user's computer, the associated change request might reflect the **In Progress** status indefinitely. If this occurs, cancel the request and then close it.  

#### To close a successful change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Completed**.  
3.  Select the change request.  
4.  In the **Tasks** pane, click **Close**.  
5.  In the **Comment** box, type a comment, and then click **OK**.  

#### To close a failed change request  

1.  In the Service Manager console, click **Work Items**.  
2.  In the **Work Items** pane, click **Change Management**, and then click **Change Requests: Failed**.  
3.  Select the change request.  
4.  In the **Tasks** pane, click **Close**.  
5.  In the **Comments** box, type a comment, and then click **OK**.  

#### To validate the closure of a change request  

-   Click the **Change Requests: Closed** view to ensure that the closed change request appears in the list.  

### Optionally send automated activity and change request notifications

You can use the following procedure to notify reviewers that an activity is available for review. You can use the second procedure to notify users that a change request has been closed.  

> [!NOTE]  
>  Only administrators can configure workflow notifications.  

#### To notify reviewers that an activity is available for review  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Workflows**, and then click **Configuration**.  
3.  Select **Activity Event Workflow Configuration**, and then click **Configure Workflow Rules** in the **Tasks** pane.  
4.  In the **Select a Class** dialog box, select **Review Activity**, and then click **OK**.  
5.  In the **Configure Workflows** dialog box, click **Add**.  
6.  In the Configure Workflows for Objects of Class Review Activity Wizard, click **Next** on the **Before You Begin** page.  
7.  On the **Workflow Information** page, type a name and a description for the workflow. In the **Check for events** list, ensure that the **When an object is updated** item is selected, and then click **Next**.  
8.  On the **Specify Criteria** page, select the **Changed From** tab. Under **Available Properties**, select **Status**, and then click **Add**.  
9. Under **Criteria**, select **Pending**, and then select the **Changed To** tab. Under **Available Properties**, select **Status**, and then click **Add**.  
10. Under **Criteria**, select **In Progress**, and then click **Next**.  
11. On the **Apply Template** page, clear the **Apply the selected template** check box, and then click **Next**.  
12. On the **Select People to Notify** page, select the **Enable notification**.  
13. Under **User**, select **Assigned To User**.  
14. Under **E\-mail Template**, if you cannot select a template, click **Create E\-Mail Template**. Otherwise, select an email notification template to apply.  
15. If you are creating an email notification template, complete the Create E\-Mail Notification Template Wizard.  
16. After you have selected an email template, click **Add**, ensure that **Reviewers** appears under the **User** column, and then click **Next**.  
17. On the **Summary** page, review the summary information, and then click **Create**.  
18. On the **Completion** page, click **Close**.  

#### To notify users that a change request has been closed  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Workflows**, and then click **Configuration**.  
3.  Select **Change Request Event Workflow Configuration**, and then click **Configure Workflow Rules** in the **Tasks** pane.  
4.  In the **Configure Workflows** dialog box, click **Add**.  
5.  In the Configure Workflows for Objects of Class Change Request Wizard, click **Next** on the **Before You Begin** page.  
6.  On the **Workflow Information** page, type a name and a description for the workflow. In the **Check for events** list, ensure that the **When an object is updated** item is selected, and then click **Next**.  
7.  On the **Specify Criteria** page, select the **Changed From** tab. Under **Available Properties**, select **Status**, and then click **Add**.  
8.  Under **Criteria**, select **Completed**.  
9. Click the **Changed To** tab.  
10. Under **Available Properties**, select **Status**, and then click **Add**.  
11. Under **Criteria**, select **Closed**, and then click **Next**.  
12. On the **Apply Template** page, clear the **Apply the selected template** check box, and then click **Next**.  
13. On the **Select People to Notify** page, select the **Enable notification** check box.  
14. Under **User**, select **Assigned To User**. Under **Template**, select **Assigned To User Notification Template**, click **Add**, and then click **Next**.  
15. On the **Summary** page, review the summary information, and then click **Create**.  
16. On the **Completion** page, click **Close**.  

#### To validate receipt of the notification  

-   The reviewer of the review activity or the user that the change request is assigned to receives an email message that indicates that a new review activity requires approval or that the change request was closed.
