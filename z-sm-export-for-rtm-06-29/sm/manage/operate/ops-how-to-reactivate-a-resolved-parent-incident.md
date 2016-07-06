---
title: How to Reactivate a Resolved Parent Incident
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a74ac01-c003-4e0f-8f91-3db3d4fd3aba
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Reactivate a Resolved Parent Incident
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], the help desk analyst  XE "Release Manager" can reactivate a parent incident, and then [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] will automatically activate all its child incidents, if the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] administrator has configured Incident settings accordingly. This method of reactivating incidents can help the analyst quickly activate many child incidents. Use the following procedure to reactivate a parent incident.  
  
 Depending on parent incident settings in the Administration workspace, behavior of automatic child incident resolution and reactivation varies. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] automatic incident resolution, see [How to Set Parent Incident Options](http://go.microsoft.com/fwlink/p/?LinkId=229704) in the Administrator’s Guide for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
### To reactivate a parent incident  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
  
2.  Select the **All Incidents** view, and then in the list of parent incidents, select the incident that you want to reactivate.  
  
3.  In the **Tasks** pane, click **Change Incident Status**, and then in the submenu, click **Activate**.  
  
4.  In the **Activate** dialog box, in the **Comments** box, type a description of the reason that you are activating the incident.  
  
5.  Click **OK** to activate the incident and child incidents, if they are available and selected, and to close the **Activate** dialog box.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)