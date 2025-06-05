---
title: Configure change and activity management
description: Provides an overview and explains how to configure change and activity management features in Service Manager.
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: 399ef0ce-7ebe-4c30-8f8a-d10f475ad49d
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
---

# Configure change and activity management in Service Manager

As part of your initial configuration of Service Manager, you've to configure settings and workflows for change and activity management. Create a change request template that you can use later when new change requests are submitted.

Configure workflows to automatically close completed change requests and send notifications to users when activities require approval. Workflows automate processes that you can use to automatically apply templates and send notifications.

A change request template is useful when you create a change request for a recurring type of issue because you can set an issue category and define a standard priority, effect, and risk level for it in the template. You can also create additional templates for other types of recurring change requests. Another benefit of creating a change request template is that users spend less time when they submit new change requests.

## Create change request templates

Use the following procedures to create two change request templates and then validate them. The first template is used to create change requests to modify Microsoft Exchange Server infrastructure. The second template is used to automatically change the priority of a standard change request to **Low**.

Change request templates store commonly used settings and apply the information to new change requests. For example, you can create a change request template that includes many activities. However, activities that you want to include in a change request template must have been previously created as activity templates.

> [!NOTE]
> When you create a change request template, don't create links to configuration items or work items, and don't enter any user information. If you create a template with these objects, you can't remove them, and you'll have to recreate the template.

### Create a messaging change request template

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, select **Templates**.
3. In the **Tasks** pane, under **Templates**, select **Create Template**.
4. In the **Create Template** dialog, enter a name for the template in the **Name** box.
   For example, enter **Changes to Messaging Infrastructure Template**.
5. In the **Description** box, enter a description for the template.
   For example, enter **Use this change template when you want to modify the messaging infrastructure**.
6. Select **Browse** to select a class.
7. In the **Select a Class** dialog, select **Change Request**, and select **OK**.
8. In the **Create Template** dialog, under **Management pack**, select **Service Manager Change Management Configuration Library**, and select **OK**.
9. In the **Change Request Template** form, on the **General** tab, in the **Description** box, enter a description for the change.
    For example, enter **Use when modifying the Exchange Server software infrastructure**.
10. In the **Area** box, select the area that is affected by the change request. 
    For example, expand **Hardware**, and then select **Server**.
11. In the **Priority** box, select a value. For example, select **High**.
12. In the **Impact** box, select a value. For example, select **Standard**.
13. In the **Risk** box, select a value. For example, select **Medium**.
14. Select the **Activities** tab, and select **Add**.
15. In the **Templates** list, select **Default Review Activity**, and select **OK** to open the review activity form.
16. In the **Title** box, enter a name for the review activity. 
    For example, enter **Messaging Infrastructure Request Approval**. Select **Add** to add the user or group that will normally approve the change request.
17. In each open form or dialog, select **OK**.

### Create a priority-modifying template

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, select **Templates**.
3. In the **Tasks** pane, select **Create Template** under **Templates**.
4. In the **Create Template** dialog, enter a name for the template in the **Name** box. For example, enter **Set Standard Change Requests to Low Priority**.
5. In the **Description** box, enter a description for the template.
   For example, enter **Use this change template to automatically set the priority for standard change requests to Low**.
6. Select **Browse** to add a class.
7. In the **Choose Class** dialog, select **Change Request**, and select **OK**.
8. In the **Create Template** dialog, under **Management pack**, select **Service Manager Change Management Configuration Library**, and select **OK**.
9. In the **Change Request Template** form, on the **General** tab, in the **Priority** list, select **Low**.
10. Select **OK**.

### Validate template creation

- Verify that the new templates were created. For example, verify that **Changes to Messaging Infrastructure Template** and **Set Standard Change Requests to Low Priority** appear in the **Templates** view. You might have to press F5 to make the new change templates appear.

## Create a manual activity template

Use the following procedures to create a manual activity template and then validate it. Manual activity templates help ensure that all manual activities are assigned to the person who is the activity implementer. After you create the manual activity template, you create a workflow that applies the template. For more information about how to create a workflow, see [How to Configure Incident Workflows](./workflows.md).

In the following procedure, you will create a manual activity template named **Set *named user* as the Activity Implementer**. This manual activity template is used in the [How to Configure Activity Management Workflows](#configure-activity-management-workflows) procedure.

### Create a manual activity template

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, select **Templates**.
3. In the **Tasks** pane, in the **Templates** area, select **Create Template**.
4. In the **Create Template** dialog, in the **Name** box, enter a name for the template. For example, enter **Set *named users* as the Activity Implementer**.
5. In the **Description** box, enter a description for the template.
6. Select **Browse** to choose a class.
7. In the **Choose Class** dialog, select **Manual Activity**, and select **OK**.
8. In the **Create Template** dialog, under **Management pack**, select **Service Manager Activity Management Configuration Library**, and select **OK**.
9. In the **Manual Activity Template** form, on the **General** tab, select the ellipsis button (**...**) next to **Activity Implementer**, select a user, and select **OK**.

### Validate that the template was created

- In the **Templates** view, verify that the new template was created. You might have to press F5 to make the new manual activity template appear.

## Configure general change settings

Use the following procedures to configure settings to specify change request prefixes and to define change request file attachment limits and then validate the settings.

> [!NOTE]
> Revising the change request prefix doesn't affect existing change requests.

To configure general change settings, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Change Request Settings**.
4. In the **Tasks** pane, in the **Change Request Settings** area, select **Properties**.
5. In the **Change Request Settings** dialog, you can make the following changes:
   - If you want to change the prefix code, change the default value in the **Change Request ID prefix** box.
   - If you want to change the maximum number of files that you can attach to a change request, change the default value in the **Maximum number of attached files** box. For example, enter **2**.
   - If you want to change the maximum size of files that you attach to a change request, change the default value in the **Maximum size (KB)** box. For example, enter **300**.
6. Select **OK** to close the **Change Request Settings** dialog.

### Validate change settings

1. To validate changes to the prefix code, create a new change request, and verify that the change request IDs have the prefix that you specified.
2. To validate changes to the attachment settings, open a change request, and attempt to add a file attachment that violates the settings that you specified.

## Configure general activity settings

Use the following procedure to configure settings to specify activity prefixes when you view activity records. You can then validate the settings. You can define these activity settings in the administrative area of the Service Manager console.

> [!NOTE]
> Revising the activity request prefix doesn't affect the existing activity records.

### Configure general activity settings

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, and select **Settings**.
3. In the **Settings** pane, select **Activity Settings**.
4. In the **Tasks** pane, in the **Activity Settings** area, select **Properties**.
5. In the **Activity Settings** dialog, you can make the following changes:
   - If you want to change the activity prefix code, change the default value in the **Activity prefix** box. For example, change the value to **AA**.
   - If you want to change the manual activity prefix code, change the default value in the **Manual activity prefix** box. For example, change the value to **AM**.
   - If you want to change the review activity prefix code, change the default value in the **Review activity prefix** box. For example, change the value to **AR**.
6. Select **OK** to close the **Activity Settings** dialog.

### Validate activity setting changes

- To validate changes to any prefix code, create a new change request, and then verify on the **Activities** tab that the activities have the new prefix that you specified.

## Configure change management workflows

Use the following procedures to set the priority of all standard change requests and then validate the change. For example, you can set the priority of all the standard change requests to low. In this procedure, you create a new workflow to automate the process.

Before you can complete the steps in the following procedures, you've to create the following templates:

- **Set Standard Change Requests to Low Priority**: For more information, see the procedure **To create a priority-modifying template** in [How to Create Change Request Templates](#create-change-request-templates).
- **New Standard Change Request Received Template**: For more information, see the procedure **To create a notification template for change requests** in [How to Create Notification Templates](./notifications.md).

### Create a workflow to set all standard change requests to low

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Workflows**, and select **Configuration**.
3. In the **Configuration** pane, select **Change Request Event Workflow Configuration**.
4. In the **Tasks** pane, in the **Change Request Event Workflow Configuration** area, select **Configure Workflow Rules**.
5. In the **Configure Workflows** dialog, select **Add**.
6. On the **Before You Begin** page of the Configure Workflows for Objects of Class Change Request Wizard, select **Next**.
7. On the **Workflow Information** page, in the **Name** box, enter a name for the workflow. For example, enter **Set Standard Change Request to Low Priority workflow**.
8. Optionally, in the **Description** box, you can enter a description of the new workflow. For example, you can enter **This workflow automatically sets the priority of a standard change request to low**.
9. In the **Check for events** list, select **When an object is created**.
10. Ensure that the **Enabled** checkbox is selected, and select **Next**.
11. On the **Specify Criteria** page, on the **Changed To** tab, in the **Related classes** list, select **Change Request**.
12. In the **Available properties** list, select **Category**, and select **Add**. In the **Criteria** area, next to the **equals** box, select **Standard**, and select **Next**.
13. On the **Apply Template** page, select the **Apply the selected template** checkbox.
14. In the **Templates** list, select **Set Standard Change Requests to Low Priority**, and select **Next**.
15. On the **Select People to Notify** page, select the **Enable notification** checkbox.
16. Under **User**, select **Created By User**, and under **Template**, select **New Standard Change Request Received Template**, and select **Add**.
17. Select **Next**.
18. On the **Summary** page, select **Create**.
19. On the **Completion** page, select **Close**.
20. In the **Configure Workflows** dialog, select **OK**.

### Validate workflow creation

1. In the **Configuration** pane, select the **Change Request Event Workflow Configuration** template.
2. In the **Tasks** pane, select **Configure Workflow Rules**.
3. In the **Configure Workflows** dialog, the **Set Standard Change Request to Low Priority workflow** workflow should appear.
4. Optionally, you can create a new change request by using the **Standard Change Request** template to verify that the priority of new requests is set to Low.
5. Notification email is sent to the user who created the change request.

## Configure activity management workflows

Use the following procedures to automatically assign all unassigned manual activities to a named user and then validate the creation of workflow.

Before you can complete the steps in the following procedures, you've to create the following templates:

- **Set *named user* as the Activity Implementer**: For more information, see [How to Create a Manual Activity Template](#create-a-manual-activity-template).
- **New Activity Assigned Received Template**: For more information, see [How to Create Notification Templates](./notifications.md).

The new workflow you're about to create applies the **Set *named user* as the Activity Implementer** template, which assigns the named user to all the activities that don't have a designated activity implementer. The **New Activity Assigned Received Template** sends notification to a user if the email notification channel is configured.

### Create an activity management workflow

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Workflows**, and select **Configuration**.
3. In the **Configuration** pane, select **Activity Event Workflow Configuration**.
4. In the **Tasks** pane, in the **Activity Event Workflow Configuration** area, select **Configure Workflow Rules**.
5. In the **Select a Class** dialog, in the **Name** list, select **Manual Activity**, and select **OK**.
6. In the **Configure Workflows** dialog, select **Add**.
7. On the **Before You Begin** page of the **Configure workflows for objects of class Manual Activity** wizard, select **Next**.
8. On the **Workflow Information** page, in the **Name** box, enter a name for the workflow. For example, enter **Assign Unassigned Activities to _named user_**.
9. Optionally, in the **Description** box, you can type a description of the new workflow. For example, you can type **This workflow automatically assigns unassigned manual activities to the _named user_**.
10. In the **Check for events** list, select **When an object is created**.
11. Ensure that the **Enabled** checkbox is selected, and select **Next**.
12. On the **Specify Criteria** page, on the **Changed to** tab, in the **Related classes** list, select **Manual Activity**.
13. In the **Available properties** list, select the **Stage** checkbox, and select **Add**.
14. In the **Criteria** area, next to the **[Activity] Stage** box, select **equals**, select **Approve** for the value, and select **Next**.
15. On the **Apply Template** page, ensure that the **Apply the selected template** checkbox is selected.
16. In the **Templates** list, select **Set *named users* as the Activity Implementer**, and select **Next**.
17. On the **Select People to Notify** page, select the **Enable notification** checkbox.
18. In the **User** list, select **Assigned to User**.
19. In the **Message template** list, select **New Activity Assigned Received Template**, select **Add**, and select **Next**.
20. On the **Summary** page, select **Create**.
21. On the **Completion** page, select **Close**.
22. In the **Configure Workflows** dialog, select **OK** to close it.

### Validate workflow creation

1. In the **Administration** pane, expand **Administration**, expand **Workflows**, and select **Status**.
2. In the **Status** pane, verify that the new workflow template titled **Assign Unassigned Activities to the _named user_** is listed.

## Next steps

[Configure settings and workflows for release management](release-mgt.md).
