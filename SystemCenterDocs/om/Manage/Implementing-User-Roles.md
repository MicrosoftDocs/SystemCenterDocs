---
title: Implementing User Roles
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Implementing User Roles

In System Center 2016 - Operations Manager, user roles are the method you use to assign the rights needed to access monitoring data and perform actions. User roles are designed to apply to groups of users that need access to and perform actions on the same group of monitored objects. By default, only the Operations Manager Administrator account has the right to view and act on monitoring data. All other users must have a user role assigned in order to view or act on monitoring data.  
  
User roles are created using the Create User Role Wizard. In this wizard, you configure which Active Directory security groups are assigned this user role, which Operations Manager group or groups of monitored objects this user can access, and which tasks and views this user role can access.  
  
A user role is the combination of a profile and scope as shown in as shown in the following illustration. A user can be a part of multiple roles and the resultant scope is the union of all the user roles.  
  
  
## Implementing User Roles topics  
  
-   [Choose a Profile](Choose-a-Profile.md)  
  
-   [Define a Scope Using Operations Manager Groups](Define-a-Scope-Using-Operations-Manager-Groups.md)  
  
-   [Assign Tasks and Views](Assign-Tasks-and-Views.md)  
  
-   [How to Assign Members to User Roles](How-to-Assign-Members-to-User-Roles.md)  
  
-   [Operations Associated with User Role Profiles](Operations-Associated-with-User-Role-Profiles.md)  
  
## Next steps

[Managing Access in Operations Manager](../../om/manage/Managing-Access-in-Operations-Manager.md)  
[Operations Manager Accounts](../Topic/Operations%20Manager%20Accounts.md)  
[How to Create a New Action Account in Operations Manager](../../om/manage/How-to-Create-a-New-Action-Account-in-Operations-Manager.md)  
[How to Manage the Report Server Unattended Execution Account in Operations Manager](../../om/manage/How-to-Manage-the-Report-Server-Unattended-Execution-Account-in-Operations-Manager.md)  
[Control Access by Using the Health Service Lockdown Tool in Operations Manager](../../om/manage/Control-Access-by-Using-the-Health-Service-Lockdown-Tool-in-Operations-Manager.md)  
[Accessing UNIX and Linux Computers in Operations Manager](../../om/manage/Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)  
[Managing Run As Accounts and Profiles](../../om/manage/Managing-Run-As-Accounts-and-Profiles.md)  
  
