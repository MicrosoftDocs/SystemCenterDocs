---
title: Approving and Modifying Change Requests
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39d5b372-f08f-402f-b80c-195f8f11d67b
---

# Approving and Modifying Change Requests

>Applies To: System Center 2016 - Service Manager

The procedures in this section describe how to approve a change request in Service Manager. Complete the following steps to approve or modify a change request.  

## How to Edit a Change Request

You can use the following procedures to edit a change request and then validate the edit. For example, you might want to change the priority of an existing change request from medium to high.  

> [!NOTE]  
>  You cannot delete an activity in a change request if the change request is in progress, however you can skip the activity or put the change request on hold and then delete the activity.  

### To edit a change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  

3.  Double\-click a change request. For example, double\-click **Apply Exchange Server Service Pack**.  

4.  Make the change that you want. For example, if you want to change the priority to high, select **High** in the **Priority** list. Or, type new text in the **Description** box.  

5.  Click **OK** to update the change request and to close it.  

### To validate an edited change request  

1.  Double\-click the change request that you updated.  

2.  Verify that your changes are displayed in the change request form.   

## How to Add a Change Reviewer

You can use the following procedures to add a change reviewer for an existing change request and then validate that the reviewer was added. You can select who reviews change requests in a way that supports your business processes. For example, if a change affects a process for which certain people are responsible, you can give those people the ability to approve change requests that affect the process.  

### To add a change reviewer  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, click **Change Management**, and then click **All Change Requests**.  

3.  Double\-click a change request to open it. For example, double\-click **Apply Exchange Server Service Pack**.  

4.  Click the **Activities** tab to view the list of manual and review activities.  

5.  Double\-click the activity to which you want to add a reviewer. The activity must have a status of **In Progress** or **Pending**, and in the ID column, the activity must also have the **RA** prefix or the prefix you defined for review activities.  

6.  In the dialog box that appears, click **Add**, type the name of a reviewer, select **Must Vote**, and then click **OK**. For example, type **Aaron Lee**.  

7.  Click **OK** to close the dialog box, and then click **OK** to update the change request and to close the form.  

### To validate that a reviewer was added  

1.  Double\-click the change request to which you added a reviewer. For example, double\-click **Apply Exchange Server Service Pack**.  

2.  Click the **Activities** tab, and then double\-click the activity to which you added a reviewer.  

3.  Verify that the reviewer was added.

## How to Approve a Review Activity Using the Console

You can use the following procedures to approve a review activity in the Service Manager console and then validate the approval. In many cases, multiple people or groups must vote to approve a single review activity before its approval is final.  

> [!NOTE]  
>  Users can only approve or reject the activities that are assigned to them.  

### To approve a review activity for a change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Review Activities**, and then click **In\-Progress Activities**.  

3.  Select a review activity. For example, select the **Messaging Infrastructure Request Approval**.  

4.  In the **Tasks** pane, click **Approve**.  

5.  In the **Comments** dialog box, type any comments that you have for the approval or rejection, and then click **OK**.  

### To validate review activity approval  

-   If all the reviewers approved the activity, the activity does not appear in the **In\-Progress Activities** view.  

-   If an activity is still in progress, it requires approval from other reviewers. Click **In\-Progress Activities**, and then open the activity to view your voting status.

## How to Send Automated Activity and Change Request Notifications

You can use the following procedure to notify reviewers that an activity is available for review. You can use the second procedure to notify users that a change request has been closed.  

> [!NOTE]  
>  Only administrators can configure workflow notifications.  

### To notify reviewers that an activity is available for review  

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

### To notify users that a change request has been closed  

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

### To validate receipt of the notification  

-   The reviewer of the review activity or the user that the change request is assigned to receives an email message that indicates that a new review activity requires approval or that the change request was closed.
