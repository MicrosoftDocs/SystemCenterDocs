---
title: Creating and Managing Groups
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Creating and Managing Groups

In System Center 2016 - Operations Manager, groups are logical collections of objects, such as Windows\-based computers, hard disks, or instances of Microsoft SQL Server. You create a group by using the Create Group Wizard. You can explicitly assign membership to a group or you can create rules that will generate a dynamic group membership.  
  
Some of the purposes for using groups are:  
  
-   To scope overrides to a specific subset of computers. 
  
-   To scope alert notifications or product connector subscriptions for a specific set of computers.   
  
-   To scope user consoles, so the user role only sees the servers they are responsible for.  
  
-   To scope a set of computers that need to go into a scheduled maintenance mode.  
  
-   To scope application views only to computers that host a given application. 
  
-   To create a rollup health state view of an otherwise unrelated set of computers. 
  
-   To create a set of computers for a report.  
  
You create and manage groups in the **Authoring** workspace of the Operations console. A number of groups are created when you install Operations Manager, and other groups may be added when you import management packs. 
  
Computer groups only contain computers. Instance groups can contain all object types, such as an instance of a health service or an instance of a SQL database. Both computer groups and instance groups can contain other computer and instance groups. Another way to view the difference between the group types is:  
  
-   An instance group is populated with objects that match your criteria.  
  
-   A computer group is populated by computers that host objects that match your criteria.  
  
Using the Operations console, you can only create instance groups. To create a computer group, you must use the Authoring console or work directly in the XML of a management pack.  
  
## Creating and Managing Groups topics  
  
-   [How to Create Groups in Operations Manager](How-to-Create-Groups-in-Operations-Manager.md)  
   
## Next steps
 
[How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)  
[How to Create a Resource Pool](How-to-Create-a-Resource-Pool.md)  


  
