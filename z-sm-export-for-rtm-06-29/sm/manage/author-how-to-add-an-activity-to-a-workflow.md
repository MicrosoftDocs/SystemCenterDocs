---
title: How to Add an Activity to a Workflow
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0995be9f-89a4-4dd0-833f-0af5bbdac846


















---
# How to Add an Activity to a Workflow
Use this procedure to add an activity to a workflow from the **Activities Toolbox** pane in the System Center 2016 - Service Manager Authoring Tool.  
  
 In the Woodgrove Bank customization scenario, Ken uses this procedure to add the Windows Workflow Foundation \(WF\) activities **Add AD DS Computer to Group** and **Set Activity Status to Completed** to his workflow.  
  
### To add an activity to a workflow  
  
1.  In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow you want, and then click **Edit**. This opens the workflow in the authoring pane. For example, right\-click **AddComputerToADGroupWF**, and then click **Edit**.  
  
2.  In the **Activities Toolbox** pane, locate the appropriate activity group.  
  
3.  Drag the activity you want to the authoring pane, and then drop it between the workflow Start and End icons or between two existing activities. The sequence of activities that is displayed in the authoring pane—from the top down—represents the order in which the activities will run. To run activities in a loop or if\-else structure, drag the structure activity \(such as [For Each Loop](../../../sm/manage/author/For-Each-Loop-Activity.md)\) onto the authoring pane first, and then drop the activities into the structure activity.  
  
     For example, drag **Add AD DS Computer to Group** from the **Active Directory Activities** group to the authoring pane, and then drop it between the workflow Start and End icons. Then, drag **Set Activity Status to Completed** and drop it between the previous activity and the End icon.  
  
4.  You can set the properties of an activity immediately after you add it to the authoring pane, or you can set the properties later.  
  
    > [!NOTE]  
    >  If you do not set the properties at this time, the activity might be marked with a Red Exclamation Point icon. This icon indicates that one or more properties of the activity must be set before the activity can run. To see a list of these required properties, click the icon.  
  
## See Also  
 [The Activity Library](../../../sm/manage/author/The-Activity-Library.md)   
 [Step 3: Create the WF Workflow](../Topic/Step%203:%20Create%20the%20WF%20Workflow.md)   
 [Adding or Removing Workflow Activities](../../../sm/manage/author/Adding-or-Removing-Workflow-Activities.md)
