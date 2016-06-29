---
title: How to Create a Parent Incident from an Incident Form
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed51d3f3-407f-4e13-aeb4-b9205f122e82
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
# How to Create a Parent Incident from an Incident Form
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], one way a help desk analyst XE "Release Manager"  can create a parent incident is when an existing incident is already opened. You can create a parent incident using the following steps. A parent incident serves as a container for several incidents.  
  
 The following procedure is performed on an incident that is neither a parent incident nor a child incident. Afterward, a new parent incident is created and the existing incident is converted to a child incident.  
  
### To create a parent incident from an incident form  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], open the Work Items workspace, and in the **Work Items** pane, expand **Incidents**.  
  
2.  Select any Incident Management view that contains active incidents, and then select an incident.  
  
3.  In the **Tasks** pane, click **Edit** to open the incident.  
  
4.  In the **Tasks** pane, click **Link to New Parent Incident** to open the **Link to New Parent Incident** dialog box.  
  
5.  In the **Link to New Parent Incident** dialog box, select a template to create the new parent incident with, and then click **OK**. For example, select **Networking Issue Incident Template**, and then click **OK**.  
  
6.  In the **Title** box, type a new description or modify the description that is inserted by the template. For example, type **Network Outage in Bldg 773.**  
  
7.  In the **Affected user** box, select the user who reported this incident. For example, select **Joe Andreshak**.  
  
8.  In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).  
  
9. The **Child Incidents** tab appears in the form where you view the child incident that the new parent incident is grouped with and where you can add other child incidents.  
  
10. In the parent incident form, click **OK** to close it.  
  
11. In the original incident form, click **OK** to close it.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)