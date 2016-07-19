---
title: Changing the Active Directory Integration Setting for an Agent
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14c847f2-448e-4140-b6d4-649ecb6e96a1
author:mgoedtel
manager:cfreemanwa
---
# Changing the Active Directory Integration Setting for an Agent
You can use the following procedure to change the Active Directory integration setting for an agent.  
  
### To change the Active Directory integration setting for an agent  
  
1.  On the agent\-managed computer, in Control Panel, double\-click Operations Manager Agent. \(In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.\)  
  
2.  On the **Management Group** tab, clear or select **Automatically update management group assignments from AD DS**. If you select this option, on agent startup, the agent will query Active Directory for a list of management groups to which it has been assigned. Those management groups, if any, will be added to the list. If you clear this option, all management groups assigned to the agent in Active Directory will be removed from the list.  
  
3.  Click **OK**.  
  
## See Also  
[Integrating Active Directory and Operations Manager](../../om/manage/Integrating-Active-Directory-and-Operations-Manager.md)  
[How to Create an Active Directory Domain Services Container for a Management Group](../../om/manage/How-to-Create-an-Active-Directory-Domain-Services-Container-for-a-Management-Group.md)  
[How to Use Active Directory Domain Services to Assign Computers to Management Servers](../../om/manage/How-to-Use-Active-Directory-Domain-Services-to-Assign-Computers-to-Management-Servers.md)  
  
