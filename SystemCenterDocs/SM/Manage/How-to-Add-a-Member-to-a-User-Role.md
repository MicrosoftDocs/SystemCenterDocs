---
title: How to Add a Member to a User Role
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1698611-409d-4856-9fce-33432e7dfd47
---
# How to Add a Member to a User Role
In Service Manager, you can assign users to a user role to define what they can do.

In this example, you have to add members of an asset management team who can create and update, but not delete, configuration items to the user role. Looking at the “Configuration Items” section of [Appendix A - List of User Role Profiles in System Center 2016 - Service Manager](Appendix-A---List-of-User-Role-Profiles-in-System-Center-2016---Service-Manager.md) in this document, you see that the Advanced Operators user role profile provides what you need regarding permissions for this team. At this time, all members of the asset management team are responsible for every asset in the company; therefore, they require unlimited scope.

Use the following procedures to add a user to the [!INCLUDE[smshort](../../includes/smshort_md.md)] Advanced Operators user role and then validate the assignment of the user to the user role.

### To assign a user to a user role

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Security**, and then select **User Roles**.

3.  In the **User Roles** pane, double\-click **Advanced Operators**.

4.  In the **Edit User Role** dialog box, click **Users**.

5.  On the **Users** page, click **Add**.

6.  In the **Select Users or Groups** dialog box, type the name of a user or group that you want to add to this user role, click **Check Names**, and then click **OK**.

7.  In the **Edit User Role** dialog box, click **OK**.

### To validate the assignment of a user to a user role

-   Log on to the [!INCLUDE[smcons](../../includes/smcons_md.md)] as one of the users assigned to the user role. Verify that you cannot access data for which you do not have access rights, as specified in the user roles.

![](Image/PSSymbol.gif)You can use a Windows PowerShell command to view users. For information about how to use Windows PowerShell to retrieve users that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)], see [Get\-SCSMUser](http://go.microsoft.com/fwlink/p/?LinkId=225335).


