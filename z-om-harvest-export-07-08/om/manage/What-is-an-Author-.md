---
title: What is an Author?
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1d13154-5661-4290-a3de-8bddee57f25f
author:markgalioto
---
# What is an Author?
A variety of management packs are available that include complete monitoring for particular applications. You can monitor these applications by installing and configuring the appropriate management pack.  
  
Operators can customize certain settings in existing monitoring configurations by using overrides. Overrides can perform such actions as disabling a particular rule, controlling how often a rule runs, or changing the threshold on a monitor. However, overrides cannot be used to create any additional monitoring.  
  
There are times where you might have to add additional monitoring scenarios to an existing management pack or create monitoring for an application or device that has no management pack. When you create new monitoring for an application, you are acting as a *Management Pack Author*. As an author, you can create additional monitoring scenarios for an application with an existing management pack or create an entirely new management pack for an application that does not have a management pack.  
  
## What tools do I use?  
Because management packs are implemented in .xml files, any XML editor can create and modify the XML code, however, this is the most complex method. Generally, you can create any monitoring that you require by using much simpler methods in the Operations console. When using the console, you have to select which management pack file you want to use to store any elements that you create, but there are few other details about the management pack that you have to consider.  
  
For more information about the tools that you can use to create a management pack, see [Authoring Tools](../../om/manage/Authoring-Tools.md).  
  
## What permissions do I require?  
The permissions that you require to perform authoring depend on the method that you are using. Permissions in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] are controlled through user roles. All authoring performed in the Operations console requires access to the **Authoring** workspace. To access this workspace, you must have the **Author** or **Administrator** user role. Your authoring credentials might be limited to particular target classes depending on the author scope of the user role. If this is the case, you only can author elements against these classes. For more information about user roles, see [Implementing User Roles](http://go.microsoft.com/fwlink/?LinkID=232869).  
  
If you are using one of the offline methods for authoring, the Authoring console or an XML editor, you do not require any permissions because you are simply creating a file offline. In contrast, to install the management pack, you must have the **Administrator** user role.  
  
## See Also  
[Authoring Tools](../../om/manage/Authoring-Tools.md)  
[Understanding Classes and Objects](../../om/manage/Understanding-Classes-and-Objects.md)  
[Implementing User Roles](http://go.microsoft.com/fwlink/?LinkID=232869)  
  
