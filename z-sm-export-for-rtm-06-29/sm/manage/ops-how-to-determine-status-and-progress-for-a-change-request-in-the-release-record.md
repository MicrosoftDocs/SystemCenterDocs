---
title: How to Determine Status and Progress for a Change Request in the Release Record
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f11a423b-58d3-4502-b9c4-b3663839984a
 

















---
# How to Determine Status and Progress for a Change Request in the Release Record
In System Center 2012 - Service Manager, the change manager reviews the status and progress of a change request in the currently opened release record. He knows the ID of the change request and its title, or at least a few of the keywords of the title. He can review the status of the change request by performing the following procedure.  
  
### To determine status and progress for a change request in a release record  
  
1.  In the Service Manager console, open the **Work Items** workspace, in the **Work Items** pane, expand **Release Management**, and then select **Release Management**.  
  
2.  In the **Work Items** pane, under **Release Management**, select the **Release Records: In Progress**.  
  
3.  In the **Release Records: In Progress** view, double\-click the record of interest to open it.  
  
4.  Click the **Activities** tab to view the list of proposed changes and dependent activities they contain. Optionally, you change the activities view by clicking either **Diagram View** or **List View**.  
  
5.  You can view records by using any of the following methods:  
  
    -   Mouse scrolling:  
  
        -   You can find the release management activity showing that it is linked to the specific change request by looking for an indicator icon and viewing its properties while in either diagram view or list view.  
  
        -   The following information is shown for all activities:  
  
            -   Activity IDs  
  
            -   Activity titles  
  
            -   Activity status indicator icons, which vary based on the state of the activity  
  
    -   Using the diagram view:  
  
        -   When you are using the diagram view, you can use **Zoom** to choose different for activities.  
  
    -   Using search anywhere in the Service Manager console:  
  
        -   You can search for and view an activity by searching with any of the following information:  
  
            -   Change request ID  
  
            -   Keywords from the linked change request’s title  
  
            -   Change activity’s ID  
  
            -   Keywords from the dependent activity’s title  
  
        -   Filtering:  
  
            -   You can filter any returned search results by keywords and also by criteria such as class, last modified dates, and name.  
  
6.  You can double\-click an activity to view its status and the details of its progress.  
  
## See Also  
 [Managing Release Records in System Center 2012 \- Service Manager](../../../sm/manage/operate/Managing-Release-Records-in-System-Center-2012---Service-Manager.md)
