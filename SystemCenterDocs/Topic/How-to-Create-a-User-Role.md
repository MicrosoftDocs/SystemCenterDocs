---
title: How to Create a User Role
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd5bcfe-2647-41c3-b84e-d42ae4509ac7
---
# How to Create a User Role
Use the following procedures to create a user role and assign users to that role in Service Manager and then validate the creation of the user role.

### To create a user role

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], select **Administration**.

2.  In the **Administration** pane, expand **Security**, and then select **User Roles**.

3.  In the **Tasks** pane under **User Roles**, select **Create User Role**, and then select the user role profile that you want to use for this user role, such as **Author**.

4.  Complete the **User Role Wizard** by doing the following:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, enter a name and description for this user role, and then click **Next**.

    3.  On the **Management Packs** page, start to filter the scope of the data that you want to assign access to. Select the management packs that contain the data that you want to assign access to, such as **Incident Management Library**. Click **Next**.

    4.  On the following pages, all the classes, queues, groups, tasks, views, and form templates that are available for the specified user role from the specified management packs, are displayed. You can select specific items on these pages to further limit the set of data that access is assigned to.

        > [!IMPORTANT]
        > The groups and the queues lists are not filtered—all groups and queues from all management packs are listed. If you select the **Select all queues** item on the **Queues** page, on the **Groups** page, **Select all Groups** is selected automatically. In addition, by default, no groups have been created. You have to create a group if you want to limit scope by group.

    5.  On the **Users** page, click **Add**, and use the **Select Users or Groups** dialog box to select users and user groups from Active Directory Domain Services \(AD DS\) for this user role, and then click **Next**.

    6.  On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    7.  On the **Completion** page, make sure that **The user role was created successfully** appears, and then click **Close**.

### To validate the creation of a user role

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], verify that the newly created user role appears in the middle pane.

2.  Log on to the [!INCLUDE[smcons](../Token/smcons_md.md)] as one of the users assigned to the user role. Verify that you cannot access data for which you do not have access rights, as specified in the user role.

![](../Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new user role in [!INCLUDE[smshort](../Token/smshort_md.md)], see [New\-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225360).

-   For information about how to use Windows PowerShell to retrieve user roles that are defined in [!INCLUDE[smshort](../Token/smshort_md.md)], see [Get\-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225343).

-   For information about how to use Windows PowerShell to set the UserRole property for a [!INCLUDE[smshort](../Token/smshort_md.md)] user, see [Update\-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225389).

-   For information about how to use Windows PowerShell to remove a user role from [!INCLUDE[smshort](../Token/smshort_md.md)], see [Remove\-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225371).

