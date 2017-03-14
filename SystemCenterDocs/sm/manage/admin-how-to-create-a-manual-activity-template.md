---
title: Create a manual activity template
description: Learn about how you can create a Service Manager manual activity template.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 09be239c-1add-4acc-ac21-a29aa080b216
---

# Create a Service Manager manual activity template

>Applies To: System Center 2016 - Service Manager

Use the following procedures to create a manual activity template and then validate it. Manual activity templates help ensure that all manual activities are assigned to the person who is the activity implementer. After you create the manual activity template, you create a workflow that applies the template. For more information about how to create a workflow, see [How to Configure Incident Workflows](admin-how-to-configure-incident-workflows.md).

In the following procedure, you will create a manual activity template named "Set *named user* as the Activity Implementer". This manual activity template is used in the [How to Configure Activity Management Workflows](admin-how-to-configure-activity-management-workflows.md) procedure.

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
