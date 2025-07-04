---
title: Manage Service Manager user roles
description: Describes the user roles used by Service Manager and how to manage them.
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: e7cd2a94-13ad-40cf-84c5-f9063072a591
ms.custom: UpdateFrequency2, engagement-fy24
---

# Manage Service Manager user roles



This section provides an overview of user roles in [List of User Role Profiles in Service Manager](user-role-profiles.md). It includes procedures that you can use to work with user roles.

## About user roles

In your organization, some employees are responsible for supporting hardware, such as portable computers and servers. Some of the employees are allowed to create and update configuration items but not delete them, whereas others are allowed to create, update, and delete configuration items.

In the [List of User Role Profiles in Service Manager](user-role-profiles.md), the security rights that allow users to access or update information are defined in a user role profile. A user role profile is a named collection of access rights, and it usually corresponds to an employee's business responsibilities. Each user role profile controls access to such artifacts as knowledge articles, work items (incidents, change requests), authoring, administration, and other credentials. Think of user role profiles as defining what you're allowed to do.

In the future, managers at your organization may decide to separate the group of employees who maintain configuration items into two groups: those who handle configuration items for desktop computers and those who handle configuration items for portable computers. They want to retain these two user role profiles, one profile that can create and edit but not delete configuration items, and another profile that can create, edit, and delete configuration items. You would define these user role profiles with different scopes, one for desktops and one for portable computers. If user role profiles define what you're allowed to do, think of scopes as defining what items you're allowed to modify. The combination of a user role profile and a scope is called a user role.

### Understand user roles

In Service Manager, when you select **Administration**, expand **Security**, and select **User Roles**, a **User Roles** pane displays a list of user roles. Each of these user roles has been configured with a user role profile and an undefined scope. Because the scope is undefined for these user roles, they can exercise their user profiles on all management packs, queues, groups, tasks, views, and form templates. The following table lists the default user roles, their associated user role profiles, and scope.

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
> The Service Manager Report Users user role is available only after you register with the Service Manager data warehouse and after the Data Warehouse navigation button is available. To view the Service Manager Report Users user role, select **Data Warehouse**, expand **Security**, and select **User Roles**.

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

### Why some user roles cannot be created

When you're creating a user role, notice that three user roles aren't available: Administrator, Report User, and Workflows. These three user roles are created and populated during Setup, and, generally speaking, these user roles are used by Service Manager. The following sections describe each of these user roles.

#### Administrator

The Administrator user role is global in scope; therefore, there's no reason for creating another user role of this type.

#### Report user

The user role, Report User, has one purpose in Service Manager: to find the computer hosting Microsoft SQL Server Reporting Services (SSRS) for the user at a Service Manager console. When a user at a Service Manager console tries to run a report, a query is made to the Service Manager management server seeking the computer that is hosting the data warehouse management server. The Service Manager console then queries the data warehouse management server seeking the name of the computer hosting SSRS. With that information, the Service Manager console connects to SSRS. The singular purpose of the user role, Report User, is to make these queries. After the Service Manager console connects to the SSRS, the credentials of the user running the console grant access as defined on the SSRS. Because of the narrow purpose of this user role, there's no reason for creating another user role.

#### Workflows

Workflows might have to read and write to the Service Manager database. During Setup, you're asked to provide credentials for the Workflows user role, and this user role performs the required actions on the Service Manager database. Like the user role, Report User, the narrow purpose of the Workflow user role means there's no reason for creating other user roles.

## Add a member to a user role

In Service Manager, you can assign users to a user role to define what they can do.

In this example, you have to add members of an asset management team who can create and update, but not delete, configuration items to the user role. Looking at the Configuration Items section of [User role profiles in Service Manager](user-role-profiles.md), you see that the Advanced Operators user role profile provides what you need regarding permissions for this team. At this time, all members of the asset management team are responsible for every asset in the company; therefore, they require unlimited scope.

Use the following procedures to add a user to the Service Manager Advanced Operators user role and then validate the assignment of the user to the user role.

### Assign a user to a user role

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Security**, and then select **User Roles**.

3. In the **User Roles** pane, double-click **Advanced Operators**.

4. In the **Edit User Role** dialog, select **Users**.

5. On the **Users** page, select **Add**.

6. In the **Select Users or Groups** dialog, enter the name of a user or group that you want to add to this user role, select **Check Names**, and select **OK**.

7. In the **Edit User Role** dialog, select **OK**.

### Validate the assignment of a user to a user role

- Sign in to the Service Manager console as one of the users assigned to the user role. Verify that you can't access data for which you don't have access rights, as specified in the user roles.

![Screenshot of the PowerShell symbol.](./media/user-roles/pssymbol.png)You can use a Windows PowerShell command to view users. For information about how to use Windows PowerShell to retrieve users that are defined in Service Manager, see [Get-SCSMUser](/previous-versions/system-center/powershell/system-center-2012-r2/hh316233(v=sc.20)).

## Create a user role

Use the following procedures to create a user role and assign users to that role in Service Manager and then validate the creation of the user role.

To create a user role, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Security**, and then select **User Roles**.

3. In the **Tasks** pane under **User Roles**, select **Create User Role**, and then select the user role profile that you want to use for this user role, such as **Author**.

4. Complete the **User Role Wizard** by doing the following:

    1. On the **Before You Begin** page, select **Next**.

    2. On the **General** page, enter a name and description for this user role, and select **Next**.

    3. On the **Management Packs** page, start to filter the scope of the data that you want to assign access to. Select the management packs that contain the data that you want to assign access to, such as **Incident Management Library**. Select **Next**.

    4. On the following pages, all the classes, queues, groups, tasks, views, and form templates that are available for the specified user role from the specified management packs, are displayed. You can select specific items on these pages to further limit the set of data that access is assigned to.

        > [!IMPORTANT]
        > The groups and the queues lists aren't filtered--all groups and queues from all management packs are listed. If you select the **Select all queues** item on the **Queues** page, on the **Groups** page, **Select all Groups** is selected automatically. In addition, by default, no groups have been created. You've to create a group if you want to limit scope by group.

    5. On the **Users** page, select **Add**, and use the **Select Users or Groups** dialog to select users and user groups from Active Directory Domain Services (AD DS) for this user role, and then select **Next**.

    6. On the **Summary** page, ensure that the settings are correct, and select **Create**.

    7. On the **Completion** page, ensure that **The user role was created successfully** appears, and select **Close**.

### Validate the creation of a user role

1. In the Service Manager console, verify that the newly created user role appears in the middle pane.

2. Sign in to the Service Manager console as one of the users assigned to the user role. Verify that you can't access data for which you don't have access rights, as specified in the user role.

![Screenshot of the PowerShell symbol.](./media/user-roles/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

- For information about how to use Windows PowerShell to create a new user role in Service Manager, see [New-SCSMUserRole](/previous-versions/system-center/powershell/system-center-2012-r2/hh316208(v=sc.20)).

- For information about how to use Windows PowerShell to retrieve user roles that are defined in Service Manager, see [Get-SCSMUserRole](/previous-versions/system-center/powershell/system-center-2012-r2/hh316218(v=sc.20)).

- For information about how to use Windows PowerShell to set the UserRole property for a Service Manager user, see [Update-SCSMUserRole](/previous-versions/system-center/powershell/system-center-2012-r2/hh316203(v=sc.20)).

- For information about how to use Windows PowerShell to remove a user role from Service Manager, see [Remove-SCSMUserRole](/previous-versions/system-center/powershell/system-center-2012-r2/hh316197(v=sc.20)).

## Next steps

- For password security requirements, password expiration, and user name changes, see [Manage Run As accounts](run-as-accounts.md).
