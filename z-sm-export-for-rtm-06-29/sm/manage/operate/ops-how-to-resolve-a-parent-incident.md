---
title: How to Resolve a Parent Incident
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e382c817-4e46-4bbb-9f7b-acb2d45f8694
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
# How to Resolve a Parent Incident
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], the help desk analyst  XE "Release Manager" can resolve a parent incident, and then [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] will automatically resolve all its child incidents, if the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] administrator has configured Incident settings accordingly. This method of resolving incidents can help the analyst quickly close many child incidents. Use the following procedure to resolve a parent incident.  
  
### To resolve a parent incident  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
  
2.  Select the **All Open Parent Incidents** view, and then in the list of parent incidents, select the incident that you want to resolve.  
  
3.  In the **Tasks** pane, click **Change Incident Status**, and then in the submenu, click **Resolve**.  
  
4.  In the **Resolve** dialog box, select a **Resolution Category**, and then in the **Comments** box, type a description of the steps that you have taken to resolve the incident.  
  
5.  If you want child incidents to resolve automatically and the option is available, ensure that the **Resolve child incidents when resolving this parent incident** option is selected, and then click **OK** to resolve the incident—and child incidents, if selected, and then close the **Resolve** dialog box.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)