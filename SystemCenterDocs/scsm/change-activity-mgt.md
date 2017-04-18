---
title:  Configure change and activity management
description: Provides an overview and explains how to configure change and activity management features in Service Manager.
manager:  carmonm
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology:  service-manager
ms.assetid:  399ef0ce-7ebe-4c30-8f8a-d10f475ad49d
---

# Configure change and activity management in Service Manager

As part of your initial configuration of Service Manager, you have to configure settings and workflows for change and activity management. Create a change request template that you can use later when new change requests are submitted.

Configure workflows to automatically close completed change requests and send notifications to users when activities require approval. Workflows automate processes that you can use to automatically apply templates and send notifications.

A change request template is useful when you create a change request for a recurring type of issue because you can set an issue category and define a standard priority, effect, and risk level for it in the template. You can also create additional templates for other types of recurring change requests. Another benefit of creating a change request template is that users spend less time when they submit new change requests.

## Create change request templates

Use the following procedures to create two change request templates and then validate them. The first template is used to create change requests to modify Microsoft Exchange Server infrastructure. The second template is used to automatically change the priority of a standard change request to **Low**.

Change request templates store commonly used settings and apply the information to new change requests. For example, you can create a change request template that includes a number of activities. However, activities that you want to include in a change request template must have been previously created as activity templates.

> [!NOTE]
> When you create a change request template, do not create links to configuration items or work items, and do not enter any user information. If you create a template with these objects, you cannot remove them, and you will have to re-create the template.

### To create a messaging change request template

1.  In the Service Manager console, click **Library**.
2.  In the **Library** pane, click **Templates**.
3.  In the **Tasks** pane, under **Templates**, click **Create Template**.
4.  In the **Create Template** dialog box, type a name for the template in the **Name** box. For example, type **Changes to Messaging Infrastructure Template**.
5.  In the **Description** box, type a description for the template.
    For example, type **Use this change template when you want to modify the messaging infrastructure**.
6.  Click **Browse** to select a class.
7.  In the **Select a Class** dialog box, click **Change Request**, and then click **OK**.
8.  In the **Create Template** dialog box, under **Management pack**, select **Service Manager Change Management Configuration Library**, and then click **OK**.
9. In the **Change Request Template** form, on the **General** tab, in the **Description** box, type a description for the change.
    For example, type **Use when modifying the Exchange Server software infrastructure**.
10. In the **Area** box, select the area that is affected by the change request. For example, expand **Hardware**, and then select **Server**.
11. In the **Priority** box, select a value. For example, select **High**.
12. In the **Impact** box, select a value. For example, select **Standard**.
13. In the **Risk** box, select a value. For example, select **Medium**.
14. Click the **Activities** tab, and then click **Add**.
15. In the **Templates** list, select **Default Review Activity**, and then click **OK** to open the review activity form.
16. In the **Title** box, type a name for the review activity. For example, type **Messaging Infrastructure Request Approval**. Then, click **Add** to add the user or group that will normally approve the change request.
17. In each open form or dialog box, click **OK**.

### To create a priority-modifying template

1.  In the Service Manager console, click **Library**.
2.  In the **Library** pane, click **Templates**.
3.  In the **Tasks** pane, click **Create Template** under **Templates**.
4.  In the **Create Template** dialog box, type a name for the template in the **Name** box. For example, type **Set Standard Change Requests to Low Priority**.
5.  In the **Description** box, type a description for the template.
    For example, type **Use this change template to automatically set the priority for standard change requests to Low**.
6.  Click **Browse** to add a class.
7.  In the **Choose Class** dialog box, click **Change Request**, and then click **OK**.
8.  In the **Create Template** dialog box, under **Management pack**, select **Service Manager Change Management Configuration Library**, and then click **OK**.
9. In the **Change Request Template** form, on the **General** tab, in the **Priority** list, select **Low**.
10. Click **OK**.

### To validate template creation

-   Verify that the new templates were created. For example, verify that **Changes to Messaging Infrastructure Template** and **Set Standard Change Requests to Low Priority** appear in the **Templates** view. You might have to press F5 to make the new change templates appear.

## Create a manual activity template

Use the following procedures to create a manual activity template and then validate it. Manual activity templates help ensure that all manual activities are assigned to the person who is the activity implementer. After you create the manual activity template, you create a workflow that applies the template. For more information about how to create a workflow, see [How to Configure Incident Workflows](config-incident-workflows.md).

In the following procedure, you will create a manual activity template named "Set *named user* as the Activity Implementer". This manual activity template is used in the [How to Configure Activity Management Workflows](config-activity-mgt-workflows.md) procedure.

### To create a manual activity template

1.  In the Service Manager console, click **Library**.
2.  In the **Library** pane, click **Templates**.
3.  In the **Tasks** pane, in the **Templates** area, click **Create Template**.
4.  In the **Create Template** dialog box, in the **Name** box, type a name for the template. For example, type **Set *named users* as the Activity Implementer**.
5.  In the **Description** box, type a description for the template.
6.  Click **Browse** to choose a class.
7.  In the **Choose Class** dialog box, click **Manual Activity**, and then click **OK**.
8.  In the **Create Template** dialog box, under **Management pack**, select **Service Manager Activity Management Configuration Library**, and then click **OK**.
9. In the **Manual Activity Template** form, on the **General** tab, click the ellipsis button (**...**) next to **Activity Implementer**, select a user, and then click **OK**.

### To validate that the template was created

-   In the **Templates** view, verify that the new template was created. You might have to press F5 to make the new manual activity template appear.

## Configure general change settings

Use the following procedures to configure settings to specify change request prefixes and to define change request file attachment limits and then validate the settings.

> [!NOTE]
> Revising the change request prefix does not affect existing change requests.

### To configure general change settings

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Change Request Settings**.
4.  In the **Tasks** pane, in the **Change Request Settings** area, click **Properties**.
5.  In the **Change Request Settings** dialog box, you can make the following changes:
    1.  If you want to change the prefix code, change the default value in the **Change Request ID prefix** box.
    2.  If you want to change the maximum number of files that you can attach to a change request, change the default value in the **Maximum number of attached files** box. For example, type **2**.
    3.  If you want to change the maximum size of files that you attach to a change request, change the default value in the **Maximum size (KB)** box. For example, type **300**.
6.  Click **OK** to close the **Change Request Settings** dialog box.

### To validate change settings

1.  To validate changes to the prefix code, create a new a change request, and verify that the change request IDs have the prefix that you specified.
2.  To validate changes to the attachment settings, open a change request, and attempt to add a file attachment that violates the settings that you specified.

## Configure general activity settings

Use the following procedure to configure settings to specify activity prefixes when you view activity records. You can then validate the settings. You can define these activity settings in the administrative area of the Service Manager console.

> [!NOTE]
> Revising the activity request prefix does not affect existing activity records.

### To configure general activity settings

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.
3.  In the **Settings** pane, click **Activity Settings**.
4.  In the **Tasks** pane, in the **Activity Settings** area, click **Properties**.
5.  In the **Activity Settings** dialog box, you can make the following changes:
    -   If you want to change the activity prefix code, change the default value in the **Activity prefix** box. For example, change the value to **AA**.
    -   If you want to change the manual activity prefix code, change the default value in the **Manual activity prefix** box. For example, change the value to **AM**.
    -   If you want to change the review activity prefix code, change the default value in the **Review activity prefix** box. For example, change the value to **AR**.
6.  Click **OK** to close the **Activity Settings** dialog box.

### To validate activity setting changes

-   To validate changes to any prefix code, create a new change request, and then verify on the **Activities** tab that the activities have the new prefix that you specified.

## Configure change management workflows

Use the following procedures to set the priority of all standard change requests and then validate the change. For example, you can set the priority of all standard change requests to low. In this procedure, you create a new workflow to automate the process.

Before you can complete the steps in the following procedures, you have to create the following templates:

-   **Set Standard Change Requests to Low Priority**: For more information, see the procedure "To create a priority-modifying template" in [How to Create Change Request Templates](create-change-req-template.md).
-   **New Standard Change Request Received Template**: For more information, see the procedure "To create a notification template for change requests" in [How to Create Notification Templates](../sm/manage/admin-how-to-create-notification-templates.md).

### To create a workflow to set all standard change requests to low

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, expand **Workflows**, and then click **Configuration**.
3.  In the **Configuration** pane, click **Change Request Event Workflow Configuration**.
4.  In the **Tasks** pane, in the **Change Request Event Workflow Configuration** area, click **Configure Workflow Rules**.
5.  In the **Configure Workflows** dialog box, click **Add**.
6.  On the **Before You Begin** page of the Configure Workflows for Objects of Class Change Request Wizard, click **Next**.
7.  On the **Workflow Information** page, in the **Name** box, type a name for the workflow. For example, type **Set Standard Change Request to Low Priority workflow**.
8.  Optionally, in the **Description** box, you can type a description of the new workflow. For example, you can type **This workflow automatically sets the priority of a standard change request to low**.
9. In the **Check for events** list, select **When an object is created**.
10. Make sure that the **Enabled** check box is selected, and then click **Next**.
11. On the **Specify Criteria** page, on the **Changed To** tab, in the **Related classes** list, select **Change Request**.
12. In the **Available properties** list, select **Category**, and then click **Add**. In the **Criteria** area, next to the **equals** box, select **Standard**, and then click **Next**.
13. On the **Apply Template** page, select the **Apply the selected template** check box.
14. In the **Templates** list, select **Set Standard Change Requests to Low Priority**, and then click **Next**.
15. On the **Select People to Notify** page, select the **Enable notification** check box.
16. Under **User**, select **Created By User**, and under **Template**, select **New Standard Change Request Received Template**, and then click **Add**.
17. Click **Next**.
18. On the **Summary** page, click **Create**.
19. On the **Completion** page, click **Close**.
20. In the **Configure Workflows** dialog box, click **OK**.

### To validate workflow creation

1.  In the **Configuration** pane, select the **Change Request Event Workflow Configuration** template.
2.  In the **Tasks** pane, click **Configure Workflow Rules**.
3.  In the **Configure Workflows** dialog box, the **Set Standard Change Request to Low Priority workflow** workflow should appear.
4.  Optionally, you can create a new change request by using the **Standard Change Request** template to verify that the priority of new requests is set to Low.
5.  Notification email is sent to the user who created the change request.

## Configure activity management workflows

Use the following procedures to automatically assign all unassigned manual activities to a named user and then validate the creation of workflow.

Before you can complete the steps in the following procedures, you have to create the following templates:

-   **Set *named user* as the Activity Implementer**: For more information, see [How to Create a Manual Activity Template](create-manual-activity.md).
-   **New Activity Assigned Received Template**: For more information, see [How to Create Notification Templates](../sm/manage/admin-how-to-create-notification-templates.md).

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
