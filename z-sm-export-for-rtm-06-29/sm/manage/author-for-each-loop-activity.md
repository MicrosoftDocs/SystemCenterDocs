---
title: For Each Loop Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e85af22-0f52-449a-aed6-eb6998028579


















---
# For Each Loop Activity
The **For Each Loop** activity takes as an input an array \(*collection*\) of objects and repeats the set of activities within the loop for each object in the collection. For example, if the input collection has five objects, the loop iterates five times. If the collection is empty, the loop does not iterate. There is no upper limit to the number of objects in the collection. The **For Each Loop** activity always runs on the computer on which the workflow runs.  
  
 The **For Each Loop** activity is a composite activity with two containers for activities:  
  
-   **Input Container**: This activity sets up the loop and defines the input collection. You can use the **Get Incident** or the **Get Virtual Machine** activity in this role.  
  
-   **Loop Container**: Named **ForEachChildActivity**, this activity contains the loop activities. Most Windows Workflow Foundation \(WF\) activities that you place in this container have two additional properties: **Current Item** and **Property to Bind**. For each activity within the loop container, set these properties as follows:  
  
    1.  Set **Current Item** to the **Current Item** property of the **Loop Container** activity of the **ForEach** activity. Note that if this activity is the first activity in the **For Each Loop** activity, **Current Item** is set automatically.  
  
    2.  Set the value of the **Property to Bind** property to the value of the property of the current activity that uses the **Current Item** value.  
  
     Two types of activities do not get the **Current Item** and **Property to Bind** properties and therefore cannot use the objects in the input collection:  
  
    -   Script activities, such as the **Windows PowerShell Script** activity.  
  
    -   Custom activities or other activities that do not inherit from the **WorkflowActivityBase** class. Such activities include those activities that are based on the **Activity** base class, such as native Visual Studio activities.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
 None.  
  
## Properties  
 The **For Each Loop** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Input Collection|InputCollection|Array\/Object|N\/A|A collection of objects to be passed, one at a time, to the activities within the **For Each Loop** activity. If the activity that resides in the input container produces an array of objects as its output property, **Input Collection** is automatically set to that property. To view the current value of this property, right\-click the loop container, and then click **Properties**.|  
|Current Item|CurrentItem|Object|N\/A|An index into **Input Collection** that activities within the loop can use as an input property. For the first activity in the loop container, this property is set automatically.|  
  
## Errors and Exceptions  
 The **For Each Loop** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions under the following conditions:  
  
-   If any error occurs in the **ForEachLoop** activity and that is not with the child activities, the workflow terminates.  
  
-   If any error occurs within the child activities, the workflow terminates unless **ContinueOnError**\=true.  
  
-   If any of the input properties are null. The activity does not iterate.  
  
 Each activity within the **For Each Loop** activity must write its own errors or exceptions to the custom tracking service. The **For Each Loop** activity does not do so itself.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [Delete Control Flow Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7643bc64-8f70-4215-8cad-e2e7901cbfad)
