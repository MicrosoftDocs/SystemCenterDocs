---
title: How to Send Automated Activity and Change Request Notifications
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0800e734-17c5-401d-be04-dcfec61a7c4b


















---
# How to Send Automated Activity and Change Request Notifications
In System Center 2012 - Service Manager, you can use the following procedure to notify reviewers that an activity is available for review. You can use the second procedure to notify users that a change request has been closed.  
  
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
  
## See Also  
 [Implementing and Closing a Change Request](../../../sm/manage/operate/Implementing-and-Closing-a-Change-Request.md)
