---
title: Choose a Profile
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: beca23da-0eb7-4f85-93a6-be48e0dd68ff
author:mgoedtel
manager:cfreemanwa
---
# Choose a Profile
Before you start the Create User Role Wizard, select one profile that applies to the user role you are creating. A profile determines the actions that a user can perform. Profiles have a defined set of rights and you cannot add or remove any of these assigned rights. When creating user roles for operators and other users, select the profile that most closely matches the responsibilities of the group of users in your [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] deployment.  
  
[!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] can monitor many types of applications in the enterprise. As the Operations Manager administrator, you want to limit access to monitoring data. Role\-based security allows you to limit privileges that users have for various aspects of Operations Manager.  
  
> [!IMPORTANT]  
> Adding a machine account to a user role member allows all services on that computer to have software development kit \(SDK\) access. It is recommended that you do not add a machine account to any user role.  
  
In Operations Manager, operations-such as resolving alerts, running tasks, overriding monitors, creating user roles, viewing alerts, viewing events, and so on-have been grouped into profiles, with each profile representing a particular job function as shown in the following table. For a list of specific operations associated with each profile, see [Operations Associated with User Role Profiles](../../om/manage/Operations-Associated-with-User-Role-Profiles.md).  
  
> [!NOTE]  
> A scope defines the entity groups, object types, tasks, or views that a profile is restricted to. Not all scopes apply to all profiles.  
  
|Profile|Job Functions and Scope|  
|-----------|---------------------------|  
|Administrator|Includes full privileges available in Operations Manager.|  
|Advanced Operator|Includes a set of privileges designed for users who need access to limited adjustment of monitoring configurations in addition to the Operator privileges. Grants members the ability to override the configuration of rules and monitors for specific targets or groups of targets within the configured scope.|  
|Application Monitoring Operator|Includes a set of privileges designed for users that need access to Application Diagnostics. A user role based on the Application Monitoring Operator profile grants members the ability to see the Application Monitoring events in Application Diagnostics web console. **Note:** Access to the **Application Advisor** feature requires the Report Operator or Administrator profile.|  
|Author|Includes a set of privileges designed for authoring of monitoring configurations. Grants members the ability to create, edit, and delete monitoring configuration \(for example, tasks, rules, monitors, and views\) for specific targets or groups of targets within the configured scope.|  
|Operator|Includes a set of privileges designed for users who need access to alerts, views, and tasks. Grants members the ability to interact with alerts, run tasks, and access views according to their configured scope. **Security Note:** When a dashboard view uses data from the data warehouse database, operators might be able to view data that they would not otherwise have access to in views that use data from the operational database.|  
|Read\-only Operator|Includes a set of privileges designed for users who need read\-only access to alerts and views. Grants members the ability to view alerts and access views according to their configured scope. **Note:** Members of the Read\-only Operator role are not assigned rights to the Task Status view. **Security Note:** When a dashboard view uses data from the data warehouse database, operators might be able to view data that they would not otherwise have access to in views that use data from the operational database.|  
|Report Operator|Includes a set of privileges designed for users who need access to Reports. Grants members the ability to view reports according to their configured scope. **Caution:** Users assigned to this role have access to all report data in the Reporting Data Warehouse and are not limited by scope.|  
|Report Security Administrator|Enables the integration of SQL Server Reporting Services security with Operations Manager user roles. This gives Operations Manager Administrators the ability to control access to reports. This role can have only one member account and cannot be scoped.|  
  
## See Also  
[Implementing User Roles](../../om/manage/Implementing-User-Roles.md)  
[Define a Scope Using Operations Manager Groups](../../om/manage/Define-a-Scope-Using-Operations-Manager-Groups.md)  
[Assign Tasks and Views](../../om/manage/Assign-Tasks-and-Views.md)  
[How to Assign Members to User Roles](../../om/manage/How-to-Assign-Members-to-User-Roles.md)  
[Operations Associated with User Role Profiles](../../om/manage/Operations-Associated-with-User-Role-Profiles.md)  
  
