---
title: How to Link an Active Incident to a Resolved Parent Incident
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d77cfdc1-8143-4729-947f-d22d80c1ac71
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
# How to Link an Active Incident to a Resolved Parent Incident
While reviewing active incidents in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], help desk analysts might determine that an incident should have already been resolved because another analyst has already corrected the underlying cause. If there is a closed parent incident, the analyst  XE "Release Manager" can use the following procedure to link the incident to the resolved parent and then automatically resolve the active incident.  
  
### To link an active incident to a resolved parent and automatically close the active incident  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
  
2.  Select any incident view that contains the incident that you want to a resolved parent to.  
  
3.  Select one or more incidents, and in the **Tasks** pane, click **Link\/Unlink to Existing Parent Incident**, and then in the submenu, click **Link**.  
  
4.  In the **Select Parent Incident** dialog box, select the resolved parent incident that you want to link the open incident to, and then click **OK**.  
  
5.  In the **Link to parent incident** dialog box, select **Link to parent and resolve incident**.  
  
6.  If you are linking multiple active incidents to a resolved parent, ensure that you select **Repeat this option for all conflicts** to automatically resolve all the incidents.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)