---
title: Define a Scope Using Operations Manager Groups
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32270078-3534-47a2-a382-81f24bd7979f
---
# Define a Scope Using Operations Manager Groups
The scope of a user role determines which objects that user role can view and perform actions on in [!INCLUDE[om12long](../Token/om12long_md.md)]. A scope is comprised of one or more Operations Manager groups and is defined when creating a user role as part of the **Create User Role Wizard**. The **Group Scope** page of the **Create User Role Wizard** provides a list of all existing Operations Manager groups. You can choose all or some of these groups as the scope of the user role you are creating.

Groups, like other Operations Manager objects, are defined in management packs. In [!INCLUDE[om12short](../Token/om12short_md.md)], groups are logical collections of objects, such as Windows\-based computers, hard disks, or instances of Microsoft SQL Server. Several groups are created by the management packs that are imported automatically during an Operations Manager installation. If these groups do not contain the monitored objects you need for a scope, you can create a group that does. To do this, you must exit the **Create User Role Wizard**, switch to the **Monitoring** workspace and use the **Create Group Wizard** to create a group that better suits your needs.

## See Also
[Implementing User Roles](../Topic/Implementing-User-Roles.md)
[Choose a Profile](../Topic/Choose-a-Profile.md)
[Assign Tasks and Views](../Topic/Assign-Tasks-and-Views.md)
[How to Assign Members to User Roles](../Topic/How-to-Assign-Members-to-User-Roles.md)

