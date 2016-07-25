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


















---
# How to Reactivate a Resolved Parent Incident
In System Center 2012 - Service Manager, the help desk analyst  XE "Release Manager" can reactivate a parent incident, and then Service Manager will automatically activate all its child incidents, if the Service Manager administrator has configured Incident settings accordingly. This method of reactivating incidents can help the analyst quickly activate many child incidents. Use the following procedure to reactivate a parent incident.  
  
 Depending on parent incident settings in the Administration workspace, behavior of automatic child incident resolution and reactivation varies. For more information about automatic incident resolution, see [How to Set Parent Incident Options](http://go.microsoft.com/fwlink/p/?LinkId=229704) in the Administrator's Guide for System Center 2012 - Service Manager.  
  
### To reactivate a parent incident  
  
1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
  
2.  Select the **All Incidents** view, and then in the list of parent incidents, select the incident that you want to reactivate.  
  
3.  In the **Tasks** pane, click **Change Incident Status**, and then in the submenu, click **Activate**.  
  
4.  In the **Activate** dialog box, in the **Comments** box, type a description of the reason that you are activating the incident.  
  
5.  Click **OK** to activate the incident and child incidents, if they are available and selected, and to close the **Activate** dialog box.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)
