---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Managing User Roles in System Center 2016   Service Manager
ms.technology:  service-manager
ms.assetid:  e7cd2a94-13ad-40cf-84c5-f9063072a591
---

# Managing User Roles in System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This section provides an overview of user roles in [Appendix A - List of User Role Profiles in Service Manager](admin-appendix-a-list-of-user-role-profiles-in-system-center-2016-service-manager.md). It includes procedures that you can use to work with user roles.

## About User Roles

In your organization, some employees are responsible for supporting hardware, such as portable computers and servers. Some of the employees are allowed to create and update configuration items but not delete them, whereas others are allowed to create, update, and delete configuration items.

In Appendix A - List of User Role Profiles Service Manager, the security rights that allow users to access or update information are defined in a user role profile. A user role profile is a named collection of access rights, and it usually corresponds to an employee's business responsibilities. Each user role profile controls access to such artifacts as knowledge articles, work items (incidents, change requests), authoring, administration, and other credentials. Think of user role profiles as defining what you are allowed to do.

In the future, managers at your organization may decide to separate the group of employees who maintain configuration items into two groups: those who handle configuration items for desktop computers and those who handle configuration items for portable computers. They want to retain these two user role profiles, one profile that can create and edit but not delete configuration items, and another profile that can create, edit, and delete configuration items. You would define these user role profiles with different scopes, one for desktops and one for portable computers. If user role profiles define what you are allowed to do, think of scopes as defining what items you are allowed to modify. The combination of a user role profile and a scope is called a user role.

### Understanding User Roles in Service Manager
In Service Manager, when you click **Administration**, expand **Security**, and then click **User Roles**, a **User Roles** pane displays a list of user roles. Each of these user roles has been configured with a user role profile and an undefined scope. Because the scope is undefined for these user roles, they can exercise their user profiles on all management packs, queues, groups, tasks, views, and form templates. The following table lists the default user roles, their associated user role profiles, and scope.

|User role|User role profile|Scope|
|-------------|---------------------|---------|
|Activity Implementers|Activity Implementer|Global|
|Administrators|Administrator|Global|
|Advanced Operators|Advanced Operator|Global|
|Change Initiators|Change Initiator|Global|
|End Users|End User|Global|
|Read-Only Operators|Read-Only Operator|Global|
|Authors|Author|Global|
|Problem Analysts|Problem Analyst|Global|
|Workflows|Workflow|Global|
|Incident Resolvers|Incident Resolver|Global|
|Change Managers|Change Manager|Global|
|Report Users|Report User|Global|
|Release Managers|Release Manager|Global|
|Service Request Analysts|Service Request Analyst|Global|

> [!NOTE]
> The Service Manager Report Users user role is available only after you register with the Service Manager data warehouse and after the Data Warehouse navigation button is available. To view the Service Manager Report Users user role, click **Data Warehouse**, expand **Security**, and then click **User Roles**.

### Example
For example, say that you want to define one security access that allows users to create and edit, but not delete, configuration items and another security access that allows users to create, edit, and delete configuration items. Appendix A, at the end of this guide, lists the user role profiles and their associated artifacts. The following table shows user role profiles as they relate to configuration items.

|User role profile|Create configuration items|Update configuration items|Delete configuration items|
|---------------------|------------------------------|------------------------------|------------------------------|
|Report User|No|No|No|
|End User|No|No|No|
|Read-Only Operator|No|No|No|
|Activity Implementer|No|No|No|
|Change Initiator|No|No|No|
|Incident Resolver|No|No|No|
|Problem Analyst|No|No|No|
|Change Manager|No|No|No|
|Advanced Operator|Yes|Yes|No|
|Author|Yes|Yes|No|
|Workflow|Yes|Yes|No|
|Administrator|Yes|Yes|Yes|

Using the previous table, you can see that the Advanced Operators user role profile can create and update, but not delete, configuration items. The Administrators user role profile can create, update, and delete configuration items. The members of the asset management team who are allowed to create and update, but not delete, configuration items are made members of the predefined  Service Manager Advanced Operators profile. The members of the asset management team who are allowed to create, edit, and delete configuration items are made members of the Administrators profile.

As a best practice, assume that members of the asset management team might change. You should create two groups in Active Directory Domain Services (AD DS) and make those groups members of the Advanced Operators and Administrators profiles. Then, as members change, users are added and removed from the Active Directory group, and no changes have to be made in Service Manager.

In the future, if you break the asset management team into two groups, one for desktops and the other for laptops, you can create your own user role by using the same user role profiles, but with different scopes.

### Why Some User Roles Cannot Be Created
When you are creating a user role, notice that three user roles are not available: Administrator, Report User, and Workflows. These three user roles are created and populated during Setup, and, generally speaking, these user roles are used by Service Manager. The following sections describe each of these user roles.

#### Administrator
The Administrator user role is global in scope; therefore, there is no reason for creating another user role of this type.

#### Report User
The user role, Report User, has one purpose in Service Manager: to find the computer hosting Microsoft SQL Server Reporting Services (SSRS) for the user at a Service Manager console. When a user at a Service Manager console tries to run a report, a query is made to the Service Manager management server seeking the computer that is hosting the data warehouse management server. The Service Manager console then queries the data warehouse management server seeking the name of the computer hosting SSRS. With that information, the Service Manager console connects to SSRS. The singular purpose of the user role, Report User, is to make these queries. After the Service Manager console connects to the SSRS, the credentials of the user running the console grant access as defined on the SSRS. Because of the narrow purpose of this user role, there is no reason for creating another user role.

#### Workflows
Workflows might have to read and write to the Service Manager database. During Setup, you are asked to provide credentials for the Workflows user role, and this user role performs the required actions on the Service Manager database. Like the user role, Report User, the narrow purpose of the Workflow user role means there is no reason for creating other user roles.

## How to Add a Member to a User Role

In Service Manager, you can assign users to a user role to define what they can do.

In this example, you have to add members of an asset management team who can create and update, but not delete, configuration items to the user role. Looking at the Configuration Items section of [Appendix A - List of User Role Profiles in Service Manager](admin-appendix-a-list-of-user-role-profiles-in-system-center-2016-service-manager.md), you see that the Advanced Operators user role profile provides what you need regarding permissions for this team. At this time, all members of the asset management team are responsible for every asset in the company; therefore, they require unlimited scope.

Use the following procedures to add a user to the Service Manager Advanced Operators user role and then validate the assignment of the user to the user role.

### To assign a user to a user role

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Security**, and then select **User Roles**.

3.  In the **User Roles** pane, double-click **Advanced Operators**.

4.  In the **Edit User Role** dialog box, click **Users**.

5.  On the **Users** page, click **Add**.

6.  In the **Select Users or Groups** dialog box, type the name of a user or group that you want to add to this user role, click **Check Names**, and then click **OK**.

7.  In the **Edit User Role** dialog box, click **OK**.

### To validate the assignment of a user to a user role

-   Log on to the Service Manager console as one of the users assigned to the user role. Verify that you cannot access data for which you do not have access rights, as specified in the user roles.

![PowerShell symbol](../media/pssymbol.png)You can use a Windows PowerShell command to view users. For information about how to use Windows PowerShell to retrieve users that are defined in Service Manager, see [Get-SCSMUser](http://go.microsoft.com/fwlink/p/?LinkId=225335).

## How to Create a User Role

Use the following procedures to create a user role and assign users to that role in Service Manager and then validate the creation of the user role.

### To create a user role

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Security**, and then select **User Roles**.

3.  In the **Tasks** pane under **User Roles**, select **Create User Role**, and then select the user role profile that you want to use for this user role, such as **Author**.

4.  Complete the **User Role Wizard** by doing the following:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, enter a name and description for this user role, and then click **Next**.

    3.  On the **Management Packs** page, start to filter the scope of the data that you want to assign access to. Select the management packs that contain the data that you want to assign access to, such as **Incident Management Library**. Click **Next**.

    4.  On the following pages, all the classes, queues, groups, tasks, views, and form templates that are available for the specified user role from the specified management packs, are displayed. You can select specific items on these pages to further limit the set of data that access is assigned to.

        > [!IMPORTANT]
        > The groups and the queues lists are not filtered--all groups and queues from all management packs are listed. If you select the **Select all queues** item on the **Queues** page, on the **Groups** page, **Select all Groups** is selected automatically. In addition, by default, no groups have been created. You have to create a group if you want to limit scope by group.

    5.  On the **Users** page, click **Add**, and use the **Select Users or Groups** dialog box to select users and user groups from Active Directory Domain Services (AD DS) for this user role, and then click **Next**.

    6.  On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    7.  On the **Completion** page, make sure that **The user role was created successfully** appears, and then click **Close**.

### To validate the creation of a user role

1.  In the Service Manager console, verify that the newly created user role appears in the middle pane.

2.  Log on to the Service Manager console as one of the users assigned to the user role. Verify that you cannot access data for which you do not have access rights, as specified in the user role.

![PowerShell symbol](../media/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new user role in Service Manager, see [New-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225360).

-   For information about how to use Windows PowerShell to retrieve user roles that are defined in Service Manager, see [Get-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225343).

-   For information about how to use Windows PowerShell to set the UserRole property for a Service Manager user, see [Update-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225389).

-   For information about how to use Windows PowerShell to remove a user role from Service Manager, see [Remove-SCSMUserRole](http://go.microsoft.com/fwlink/p/?LinkId=225371).
