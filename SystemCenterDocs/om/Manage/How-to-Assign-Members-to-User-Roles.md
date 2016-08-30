---
title: How to Assign Members to User Roles
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Assign Members to User Roles

System Center 2016 - Operations Manager provides eight standard user roles that are created during setup. You can assign groups and individuals to these built\-in user roles to provide them with the ability to perform certain tasks and to access certain information.  
  
The following table describes the built\-in user roles, which have global scope for the management group. To limit the scope for a user, create a new user role. For more information, see [Implementing User Roles](Implementing-User-Roles.md).  
  
> [!IMPORTANT]  
> When you add a group to the Operations Manager Administrators user role, you must restart the management server for the change to take effect.  
  
|User role|Description|  
|-------------|---------------|  
|Administrator|Has full privileges to all Operations Manager data, services, and tools. **Note:** You can only add Active Directory security groups to the Administrator role.|  
|Advanced Operator|Has limited change access to Operations Manager configuration; ability to create overrides to rules; monitors for targets or groups of targets within the configured scope. Advanced Operator also inherits Operator privileges.|  
|Application Monitoring Operator|Includes a set of privileges designed for users that need access to **Application Diagnostics**. The Application Monitoring Operator user role grants members the ability to see the Application Monitoring events in **Application Diagnostics**.|  
|Author|Has ability to create, edit, and delete tasks, rules, monitors, and views within configured scope. Author also inherits Advanced Operator privileges.|  
|Operator|Has ability to edit or delete alerts, run tasks, and access views according to configured scope. Operator also inherits Read\-Only Operator privileges. **Security Note:** When a dashboard view uses data from the data warehouse database, operators might be able to view data that they would not otherwise have access to in views that use data from the operational database.|  
|Read\-Only Operator|Has ability to view alerts and access views according to configured scope. **Security Note:** When a dashboard view uses data from the data warehouse database, operators might be able to view data that they would not otherwise have access to in views that use data from the operational database.|  
|Report Operator|Has ability to view reports according to configured scope.|  
|Report Security Administrator|Enables integration of SQL Reporting Services security with Operations Manager roles.|  
  
### To assign members to user roles  
  
1.  In the Operations console, click **Administration**.  
  
2.  In **Security**, click **User Roles**.  
  
3.  In the results pane, right\-click any of the user roles, such as **Operations Manager Operators**, and click **Properties**.  
  
4.  On the **General Properties** tab, in **User role members**, click **Add**.  
  
5.  In **Enter the object names to select**, type in name of the user or group account that you want to add to the user role, and then click **OK** to close the dialog box.  
  
6.  Click **OK** to close the properties for the user role.  
  

  
