---
title: How to Add a Control Flow Activity to a Workflow
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a554c4af-4d94-400d-82a6-d9ca08ecb6d6


















---
# How to Add a Control Flow Activity to a Workflow
Use control flow activities to provide structure—branches, loops, or timer delays—for your workflow. The System Center 2016 - Service Manager Authoring Tool provides four built\-in control flow activities:  
  
-   **[Delay Activity](../../../sm/manage/author/Delay-Activity.md)** : Introduces a delay between activities in a workflow.  
  
-   **[For Each Loop Activity](../../../sm/manage/author/For-Each-Loop-Activity.md)** : Takes as an input an array \(*collection*\) of objects, and repeats the set of activities in the **For Each Loop** object in the collection.  
  
-   **[IfElse Activity](../../../sm/manage/author/IfElse-Activity.md)** : Controls the sequence of activities in a workflow based on a Boolean \(True\/False\) condition.  
  
-   **[Parallel Activity](../../../sm/manage/author/Parallel-Activity.md)** : Forks the sequence of activities into two simultaneous sequences of activities.  
  
 To use a **Delay** activity, just drag the **Delay** activity into the workflow, and then set the activity’s **TimeoutDuration** property to the delay interval you want to use. To use an **IfElse** or **Parallel** activity, drag the activity into the workflow, and then drop regular activities into the **IfElse** or **Parallel** activity.  
  
 Using a **For Each Loop** activity resembles using an **IfElse** or **Parallel** activity; however, you might want to set additional properties for the activities in the **For Each Loop**. Use the following procedure to add a **For Each Loop** to a workflow.  
  
### To add a For Each Loop to a workflow  
  
1.  In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow you want, and then click **Edit**. This opens the workflow in the authoring pane.  
  
2.  In the **Activities Toolbox** pane, locate the activity group **Control Flow**.  
  
3.  Drag the **For Each Loop** activity to a position between the Workflow Start and Workflow End icons or between two existing activities.  
  
4.  Add the activities for which you want to loop the execution to the **Loop Container\(ForEachChildActivity\)**. To add each activity:  
  
    1.  In the **Activities Toolbox** pane, expand the activity group that contains the activity that you want to use.  
  
    2.  Drag the activity to a position to the top of the **Loop Container** activity. If the **Loop Container** activity already contains other activities, drag the new activity to a position before, after, or between the existing activities.  
  
    3.  Most workflow activities that you place in this container have two additional properties: **Current Item** and **Property to Bind**. For each activity within the loop container, set these properties as follows:  
  
        > [!NOTE]  
        >  Setting the properties is not mandatory, and it is useful only if you want to take the object from the **Input Collection** of the **Loop Container**.  
  
        1.  Set **Current Item** to the **Current Item** property of the **Loop Container** activity of the **ForEach** activity. Note that, if this activity is the first activity in the **For Each Loop**, **Current Item** is set automatically.  
  
        2.  Set the value of the **Property to Bind** property to the value of the property of the current activity that will use the **Current Item** value.  
  
## See Also  
 [Adding or Removing Workflow Activities](../../../sm/manage/author/Adding-or-Removing-Workflow-Activities.md)
