---
title: How to Create Change Request Templates
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d0d4e7e-e1c4-413b-b5fd-2404973fe026
---
# How to Create Change Request Templates

>Applies To: System Center 2016 Technical Preview - Service Manager

Use the following procedures to create two change request templates and then validate them. The first template is used to create change requests to modify Microsoft Exchange Server infrastructure. The second template is used to automatically change the priority of a standard change request to **Low**. For more information about how to use the second template after you create it, see [How to Configure Change Management Workflows](How-to-Configure-Change-Management-Workflows.md).

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



