---
title: Implementing and Closing a Change Request
manager: cfreeman
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
ms.assetid: 61d3e06a-be67-4203-a47b-a6af1a01702a
---

# Implementing and Closing a Change Request

>Applies To: System Center 2016 - Service Manager

The procedures in this section describe how to implement and close a change request in Service Manager.  

 Complete the following steps to implement and close a change request.  

## How to Complete or Fail a Manual Activity

You can use the following procedures to complete or fail a manual activity in Service Manager and then validate that the manual activity is complete or failed.  

### To successfully complete a manual activity  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and then click **In\-Progress Activities**.  

3.  Select the manual activity.  

4.  In the **Tasks** pane, click **Mark as Completed**.  

5.  In the **Comments** box, type a comment, and then click **OK**.  

### To fail a manual activity  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and then click **In\-Progress Activities**.  

3.  Select the manual activity.  

4.  In the **Tasks** pane, click **Mark as Failed**.  

5.  In the **Comments** box, type a comment, and then click **OK**. For example, type **The post\-implementation analysis indicates that the new hardware does not adequately meet our needs and has failed the review**.  

### To validate that a manual activity is complete or failed  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and then click **All Activities**.  

3.  Verify that the manual activity is set to either **Completed** or **Failed**.  

## How to Close a Change Request

You can use the following procedures to permanently close a successful change request or a failed change request and then validate the closure of the change request. You cannot reopen a closed change request.  

> [!NOTE]  
>  If an end user cancels a software request before the software is deployed to the end user's computer, the associated change request might reflect the **In Progress** status indefinitely. If this occurs, cancel the request and then close it.  

### To close a successful change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Completed**.  

3.  Select the change request.  

4.  In the **Tasks** pane, click **Close**.  

5.  In the **Comment** box, type a comment, and then click **OK**.  

### To close a failed change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, click **Change Management**, and then click **Change Requests: Failed**.  

3.  Select the change request.  

4.  In the **Tasks** pane, click **Close**.  

5.  In the **Comments** box, type a comment, and then click **OK**.  

### To validate the closure of a change request  

-   Click the **Change Requests: Closed** view to ensure that the closed change request appears in the list.  

## Optionally Send Automated Activity and Change Request Notifications

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
