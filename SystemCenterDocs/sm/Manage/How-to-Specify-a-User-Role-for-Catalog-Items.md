---
title: How to Specify a User Role for Catalog Items
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85ce5254-2a03-4e37-8e8c-072b263c7e51
---
# How to Specify a User Role for Catalog Items

>Applies To: System Center 2016 Technical Preview - Service Manager

User roles provide access to catalog groups that contain catalog items. Both service offerings and their request offerings are available to Self-Service Portal users, when the status of the offerings is set to Published and if end users have been assigned a corresponding Service Manager user role. Only users who have been assigned a user role associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog. You can use the following procedure to create a user role and associate catalog items and users with the role.

### To create a user role and associate it with catalog items and users

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Security**, and then select **User Roles**.

3.  In the **Tasks** pane under **User Roles**, click **Create User Role**, and then click **End User** to open the Create User Role Wizard.

4.  On the **Before You Begin** page, read the instructions, and then click **Next**.

5.  On the **General** page, complete these steps:

    1.  In the **Name** box, type a name for the user role. For example, type **Security Offerings End User Role**.

    2.  Optionally, in the **Description** box, type a description of the purpose of the user role. For example, type **This user role provides access to security offerings to end users**.

    3.  Click **Next**.

6.  On the **Management Packs** page, complete these steps:

    1.  In **Management Packs** list, select a management pack that is used by catalog items. For example, select **Service Manager Service Request Configuration Library**.

    2.  Click **Next**.

7.  On the **Queues** page, there are no options that apply to security to catalog items; therefore, click **Next**.

8.  On the **Configuration Item Groups** page, there are no options that apply to security to catalog items; therefore, click **Next**.

9. On the **Catalog Item Groups** page, select **Provide access to only the selected groups**, select the groups that you want to provide access to, and then click **Next**.

10. On the **Form Templates** page, ensure that **All forms can be accessed** is selected, and then click **Next**.

11. On the **Users** page, add the users and groups that you want to provide access to, and then click **Next**.

12. On the **Summary** page, review the information, and then click **Create**.

13. On the **Completion** page, click **Close**.



