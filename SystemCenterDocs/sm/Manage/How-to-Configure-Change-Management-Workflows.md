---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Configure Change Management Workflows
ms.technology:  service-manager
ms.assetid:  8a9d5a24-c13c-4db2-a3b4-6b728a20e3c6
---

# How to Configure Change Management Workflows

>Applies To: System Center 2016 Technical Preview - Service Manager

Use the following procedures to set the priority of all standard change requests and then validate the change. For example, you can set the priority of all standard change requests to low. In this procedure, you create a new workflow to automate the process.

Before you can complete the steps in this procedure, you have to create the following templates:

-   **Set Standard Change Requests to Low Priority**: For more information, see the procedure "To create a priority-modifying template" in [How to Create Change Request Templates](How-to-Create-Change-Request-Templates.md).

-   **New Standard Change Request Received Template**: For more information, see the procedure "To create a notification template for change requests" in [How to Create Notification Templates](How-to-Create-Notification-Templates.md).

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



