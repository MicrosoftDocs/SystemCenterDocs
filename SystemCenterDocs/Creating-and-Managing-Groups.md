---
title: Creating and Managing Groups
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5702352-bcaa-4a89-85ca-78fff15019e2
---
# Creating and Managing Groups
In [!INCLUDE[om12long](Token/om12long_md.md)], groups are logical collections of objects, such as Windows\-based computers, hard disks, or instances of Microsoft SQL Server. You create a group by using the Create Group Wizard. You can explicitly assign membership to a group or you can create rules that will generate a dynamic group membership.

Some of the purposes for using groups are:

-   To scope overrides to a specific subset of computers. For more information, see [Using Classes and Groups for Overrides in Operations Manager](Using-Classes-and-Groups-for-Overrides-in-Operations-Manager.md).

-   To scope alert notifications or product connector subscriptions for a specific set of computers. [How to Create Subscriptions Using Classes and Groups](How-to-Create-Subscriptions-Using-Classes-and-Groups.md)

-   To scope user consoles, so the user role only sees the servers they are responsible for.

-   To scope a set of computers that need to go into a scheduled maintenance mode.

-   To scope application views only to computers that host a given application. For more information, see [Guidance for Scoping and Targeting Views](Guidance-for-Scoping-and-Targeting-Views.md).

-   To create a rollup health state view of an otherwise unrelated set of computers. For more information, see [Guidance for Scoping and Targeting Views](Guidance-for-Scoping-and-Targeting-Views.md).

-   To create a set of computers for a report.

You create and manage groups in the **Authoring** workspace of the Operations console. A number of groups are created when you install Operations Manager, and other groups may be added when you import management packs. The following image shows the display of groups in the Operations console.

![](7343bbe6-80a7-40cb-b12b-f5b7d289b3a8)

The icons differentiate between computer groups and instance groups, as shown in the following image.

![](9879c69d-ad3b-4b00-9d64-2f3c84118622)

Computer groups only contain computers. Instance groups can contain all object types, such as an instance of a health service or an instance of a SQL database. Both computer groups and instance groups can contain other computer and instance groups. Another way to view the difference between the group types is:

-   An instance group is populated with objects that match your criteria.

-   A computer group is populated by computers that host objects that match your criteria.

Using the Operations console, you can only create instance groups. To create a computer group, you must use the Authoring console or work directly in the XML of a management pack.

## Creating and Managing Groups topics

-   [How to Create Groups in Operations Manager](How-to-Create-Groups-in-Operations-Manager.md)

-   [How to View Group Members, State, and Diagram](How-to-View-Group-Members,-State,-and-Diagram.md)

## Other resources for this component

-   [TechNet Library main page for Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=223634)

-   [Operations Guide for System Center 2012 - Operations Manager](Operations-Guide-for-System-Center-2012---Operations-Manager.md)

-   [General Tasks in Operations Manager_1](General-Tasks-in-Operations-Manager_1.md)

-   [How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)

-   [Managing Alerts](Managing-Alerts.md)

-   [Running Tasks in Operations Manager](Running-Tasks-in-Operations-Manager.md)

-   [How to Create a Resource Pool](How-to-Create-a-Resource-Pool.md)

-   [Connecting Management Groups in Operations Manager](Connecting-Management-Groups-in-Operations-Manager.md)

-   [Operations Manager Report Authoring Guide](http://go.microsoft.com/fwlink/p/?LinkID=217092)

## See Also
[General Tasks in Operations Manager_1](General-Tasks-in-Operations-Manager_1.md)
[Managing Alerts](Managing-Alerts.md)
[How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)
[Using Operations Manager Shell](Using-Operations-Manager-Shell.md)
[Running Tasks in Operations Manager](Running-Tasks-in-Operations-Manager.md)
[How to Create a Resource Pool](How-to-Create-a-Resource-Pool.md)
[Managing Resource Pools for UNIX and Linux Computers](Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)
[Connecting Management Groups in Operations Manager](Connecting-Management-Groups-in-Operations-Manager.md)


