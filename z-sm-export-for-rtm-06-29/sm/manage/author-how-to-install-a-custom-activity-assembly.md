---
title: How to Install a Custom Activity Assembly
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1ce34df3-e6c7-458f-9224-1f5e54a75fc6


















---
# How to Install a Custom Activity Assembly
So that you can use custom or third\-party Windows Workflow Foundation \(WF\)  activities in workflows, the activity assembly files must first be installed. You must have administrative permissions on the computer running the System Center 2016 - Service Manager Authoring Tool and the computer running Service Manager. Like the default activities, custom activities must be available on the computer running Service Manager as well as on the computer running the Authoring Tool.  
  
### To install a custom activity assembly  
  
1.  On the computer running the Authoring Tool, browse to the Authoring Tool Workflow Activity Library folder, for example, D:\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2012 Authoring\\Workflow Activity Library. Paste the custom activity assembly into this folder.  
  
2.  On the computer running Service Manager, browse to the Service Manager installation folder, and then paste the custom activity assembly into this folder.  
  
3.  After you have installed the custom activity assembly, notify the Authoring Tool users that they can now add the custom activities to personalized activity groups, by using the following procedures:  
  
    > [!NOTE]  
    >  Users can only add custom activities to personalized activity groups; they cannot add custom activities to the default activity groups.  
  
    1.  [How to Create a Personalized Activity Group](../../../sm/manage/author/How-to-Create-a-Personalized-Activity-Group.md) provides instructions for creating a personalized activity group.  
  
    2.  [How to Add Activities to a Personalized Activity Group](../../../sm/manage/author/How-to-Add-Activities-to-a-Personalized-Activity-Group.md) provides instructions for adding custom activities to a personalized activity group.  
  
## See Also  
 [How to Create a Personalized Activity Group](../../../sm/manage/author/How-to-Create-a-Personalized-Activity-Group.md)   
 [How to Add Activities to a Personalized Activity Group](../../../sm/manage/author/How-to-Add-Activities-to-a-Personalized-Activity-Group.md)   
 [Modifying the Default Toolbox](../../../sm/manage/author/Modifying-the-Default-Toolbox.md)
