---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
title:  How to Configure Activity Management Workflows
ms.technology:  service-manager
ms.assetid:  2d7b2743-e25d-4a96-9c2d-35406c5ec279
---

# How to Configure Activity Management Workflows

>Applies To: System Center 2016 - Service Manager

Use the following procedures to automatically assign all unassigned manual activities to a named user and then validate the creation of workflow.

Before you can complete the steps in this procedure, you have to create the following templates:

-   **Set *named user* as the Activity Implementer**: For more information, see [How to Create a Manual Activity Template](admin-how-to-create-a-manual-activity-template.md).

-   **New Activity Assigned Received Template**: For more information, see [How to Create Notification Templates](admin-how-to-create-notification-templates.md).

The new workflow you are about to create applies the **Set *named user* as the Activity Implementer** template, which assigns the named user all the activities that do not have a designated activity implementer. The **New Activity Assigned Received Template** sends notification to a user if the email notification channel is configured.

### To create an activity management workflow

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Workflows**, and then click **Configuration**.

3.  In the **Configuration** pane, click **Activity Event Workflow Configuration**.

4.  In the **Tasks** pane, in the **Activity Event Workflow Configuration** area, click **Configure Workflow Rules**.

5.  In the **Select a Class** dialog box, in the **Name** list, select **Manual Activity**, and then click **OK**.

6.  In the **Configure Workflows** dialog box, click **Add**.

7.  On the **Before You Begin** page of the **Configure workflows for objects of class Manual Activity** wizard, click **Next**.

8.  On the **Workflow Information** page, in the **Name** box, type a name for the workflow. For example, type **Assign Unassigned Activities to *named user***.

9. Optionally, in the **Description** box, you can type a description of the new workflow. For example, you can type **This workflow automatically assigns unassigned manual activities to the *named user***.

10. In the **Check for events** list, select **When an object is created**.

11. Make sure that the **Enabled** check box is selected, and then click **Next**.

12. On the **Specify Criteria** page, on the **Changed to** tab, in the **Related classes** list, select **Manual Activity**.

13. In the **Available properties** list, select the **Stage** check box, and then click **Add**.

14. In the **Criteria** area, next to the **[Activity] Stage** box, select **equals**, select **Approve** for the value, and then click **Next**.

15. On the **Apply Template** page, make sure that **Apply the selected template** check box is selected.

16. In the **Templates** list, select **Set *named users* as the Activity Implementer**, and then click **Next**.

17. On the **Select People to Notify** page, select the **Enable notification** check box.

18. In the **User** list, select **Assigned to User**.

19. In the **Message template** list, select **New Activity Assigned Received Template**, click **Add**, and then click **Next**.

20. On the **Summary** page, click **Create**.

21. On the **Completion** page, click **Close**.

22. In the **Configure Workflows** dialog box, click **OK** to close it.

### To validate workflow creation

1.  In the **Administration** pane, expand **Administration**, expand **Workflows**, and then click **Status**.

2.  In the **Status** pane, verify that the new workflow template titled **Assign Unassigned Activities to the *named user*** is listed.
