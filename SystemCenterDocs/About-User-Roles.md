---
title: About User Roles
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98ff2c1f-28d5-42fb-9dcf-47707e4d6620
---
# About User Roles
In your organization, some employees are responsible for supporting hardware, such as portable computers and servers. Some of the employees are allowed to create and update configuration items but not delete them, whereas others are allowed to create, update, and delete configuration items.

In Appendix A - List of User Role Profiles in System Center 2016 - Service Manager, the security rights that allow users to access or update information are defined in a user role profile. A user role profile is a named collection of access rights, and it usually corresponds to an employee’s business responsibilities. Each user role profile controls access to such artifacts as knowledge articles, work items \(incidents, change requests\), authoring, administration, and other credentials. Think of user role profiles as defining what you are allowed to do.

In the future, managers at your organization may decide to separate the group of employees who maintain configuration items into two groups: those who handle configuration items for desktop computers and those who handle configuration items for portable computers. They want to retain these two user role profiles, one profile that can create and edit but not delete configuration items, and another profile that can create, edit, and delete configuration items. You would define these user role profiles with different scopes, one for desktops and one for portable computers. If user role profiles define what you are allowed to do, think of scopes as defining what items you are allowed to modify. The combination of a user role profile and a scope is called a user role.

## Understanding User Roles in Service Manager
In [!INCLUDE[smshort]./Token/smshort_md.md)], when you click **Administration**, expand **Security**, and then click **User Roles**, a **User Roles** pane displays a list of user roles. Each of these user roles has been configured with a user role profile and an undefined scope. Because the scope is undefined for these user roles, they can exercise their user profiles on all management packs, queues, groups, tasks, views, and form templates. The following table lists the default user roles, their associated user role profiles, and scope.

|User role|User role profile|Scope|
|-------------|---------------------|---------|
|Activity Implementers|Activity Implementer|Global|
|Administrators|Administrator|Global|
|Advanced Operators|Advanced Operator|Global|
|Change Initiators|Change Initiator|Global|
|End Users|End User|Global|
|Read\-Only Operators|Read\-Only Operator|Global|
|Authors|Author|Global|
|Problem Analysts|Problem Analyst|Global|
|Workflows|Workflow|Global|
|Incident Resolvers|Incident Resolver|Global|
|Change Managers|Change Manager|Global|
|Report Users|Report User|Global|
|Release Managers|Release Manager|Global|
|Service Request Analysts|Service Request Analyst|Global|

> [!NOTE]
> The [!INCLUDE[smshort]./Token/smshort_md.md)] Report Users user role is available only after you register with the [!INCLUDE[smshort]./Token/smshort_md.md)] data warehouse and after the Data Warehouse navigation button is available. To view the [!INCLUDE[smshort]./Token/smshort_md.md)] Report Users user role, click **Data Warehouse**, expand **Security**, and then click **User Roles**.

## Example
For example, say that you want to define one security access that allows users to create and edit, but not delete, configuration items and another security access that allows users to create, edit, and delete configuration items. Appendix A, at the end of this guide, lists the user role profiles and their associated artifacts. The following table shows user role profiles as they relate to configuration items.

|User role profile|Create configuration items|Update configuration items|Delete configuration items|
|---------------------|------------------------------|------------------------------|------------------------------|
|Report User|No|No|No|
|End User|No|No|No|
|Read\-Only Operator|No|No|No|
|Activity Implementer|No|No|No|
|Change Initiator|No|No|No|
|Incident Resolver|No|No|No|
|Problem Analyst|No|No|No|
|Change Manager|No|No|No|
|Advanced Operator|Yes|Yes|No|
|Author|Yes|Yes|No|
|Workflow|Yes|Yes|No|
|Administrator|Yes|Yes|Yes|

Using the previous table, you can see that the Advanced Operators user role profile can create and update, but not delete, configuration items. The Administrators user role profile can create, update, and delete configuration items. The members of the asset management team who are allowed to create and update, but not delete, configuration items are made members of the predefined  [!INCLUDE[smshort]./Token/smshort_md.md)] Advanced Operators profile. The members of the asset management team who are allowed to create, edit, and delete configuration items are made members of the Administrators profile.

As a best practice, assume that members of the asset management team might change. You should create two groups in Active Directory Domain Services \(AD DS\) and make those groups members of the Advanced Operators and Administrators profiles. Then, as members change, users are added and removed from the Active Directory group, and no changes have to be made in [!INCLUDE[smshort]./Token/smshort_md.md)].

In the future, if you break the asset management team into two groups, one for desktops and the other for laptops, you can create your own user role by using the same user role profiles, but with different scopes.

## Why Some User Roles Cannot Be Created
When you are creating a user role, notice that three user roles are not available: Administrator, Report User, and Workflows. These three user roles are created and populated during Setup, and, generally speaking, these user roles are used by [!INCLUDE[smshort]./Token/smshort_md.md)]. The following sections describe each of these user roles.

### Administrator
The Administrator user role is global in scope; therefore, there is no reason for creating another user role of this type.

### Report User
The user role, Report User, has one purpose in [!INCLUDE[smshort]./Token/smshort_md.md)]: to find the computer hosting Microsoft SQL Server Reporting Services \(SSRS\) for the user at a [!INCLUDE[smcons]./Token/smcons_md.md)]. When a user at a [!INCLUDE[smcons]./Token/smcons_md.md)] tries to run a report, a query is made to the [!INCLUDE[smshort]./Token/smshort_md.md)] management server seeking the computer that is hosting the data warehouse management server. The [!INCLUDE[smcons]./Token/smcons_md.md)] then queries the data warehouse management server seeking the name of the computer hosting SSRS. With that information, the [!INCLUDE[smcons]./Token/smcons_md.md)] connects to SSRS. The singular purpose of the user role, Report User, is to make these queries. After the [!INCLUDE[smcons]./Token/smcons_md.md)] connects to the SSRS, the credentials of the user running the console grant access as defined on the SSRS. Because of the narrow purpose of this user role, there is no reason for creating another user role.

### Workflows
Workflows might have to read and write to the [!INCLUDE[smshort]./Token/smshort_md.md)] database. During Setup, you are asked to provide credentials for the Workflows user role, and this user role performs the required actions on the [!INCLUDE[smshort]./Token/smshort_md.md)] database. Like the user role, Report User, the narrow purpose of the Workflow user role means there is no reason for creating other user roles.



