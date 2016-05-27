---
title: How to Create a Manual Activity Template
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09be239c-1add-4acc-ac21-a29aa080b216
---
# How to Create a Manual Activity Template
Use the following procedures to create a manual activity template and then validate it. Manual activity templates help ensure that all manual activities are assigned to the person who is the activity implementer. After you create the manual activity template, you create a workflow that applies the template. For more information about how to create a workflow, see [How to Configure Incident Workflows](How-to-Configure-Incident-Workflows.md).

In the following procedure, you will create a manual activity template named "Set \<named user\> as the Activity Implementer". This manual activity template is used in the [How to Configure Activity Management Workflows](How-to-Configure-Activity-Management-Workflows.md) procedure.

### To create a manual activity template

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Library**.

2.  In the **Library** pane, click **Templates**.

3.  In the **Tasks** pane, in the **Templates** area, click **Create Template**.

4.  In the **Create Template** dialog box, in the **Name** box, type a name for the template. For example, type **Set \<named users\> as the Activity Implementer**.

5.  In the **Description** box, type a description for the template.

6.  Click **Browse** to choose a class.

7.  In the **Choose Class** dialog box, click **Manual Activity**, and then click **OK**.

8.  In the **Create Template** dialog box, under **Management pack**, select **Service Manager Activity Management Configuration Library**, and then click **OK**.

9. In the **Manual Activity Template** form, on the **General** tab, click the ellipsis button \(**…**\) next to **Activity Implementer**, select a user, and then click **OK**.

### To validate that the template was created

-   In the **Templates** view, verify that the new template was created. You might have to press F5 to make the new manual activity template appear.


