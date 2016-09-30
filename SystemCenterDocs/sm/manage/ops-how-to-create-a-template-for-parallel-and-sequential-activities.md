---
title: How to Create a Template for Parallel and Sequential Activities
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 83ad5318-aca4-4e87-b11c-a287ad9e73e1
---

# How to Create a Template for Parallel and Sequential Activities

>Applies To: System Center 2016 - Service Manager

Release record templates for parallel and sequential activities are used to create new activities that contain a collection of predefined activities that should be grouped together to form some kind of process. You can think of parallel and sequential activities as container activities because their primary function is to contain individual activities.  

 The template author creates a template for a parallel activity by performing the following procedure. Afterward, the same steps are followed to create a template for a sequential activity.  

### To create a template for a parallel activity  

1.  In the Service Manager console, open the **Library** workspace, and in the **Library** pane, select **Templates**.  

2.  In the **Templates** list, select **Default Parallel Activity**, and then in the **Tasks** pane under **Templates**, click **Create Template**.  

3.  In the **Create Template** dialog box, type a name for the template and a description of what the template applies.  

4.  Under **Class**, click **Browse**, in the **Select a Class** box, select **Parallel Activity**, and then click **OK** to close the **Select a Class** box.  

5.  Click **OK** to close the **Create Template** dialog box, and the New Container Activity Template form appears.  

6.  Enter information in the boxes on the **General** tab, and then click the **Activities** tab.  

7.  You can add, delete, or modify sets of activities to the parallel activity template, including the following actions:  

    1.  Add activities from the list of existing activity templates.  

    2.  Add parallel or sequential activities from the list of existing activity templates.  

    3.  Move activities up and down in the order in which they are completed.  

    4.  Move activities in the process list.  

    5.  Delete activities.  

8.  As you add an activity, the activity form opens. Enter necessary information, and then click **OK** to save the activity.  

9. When you have added all the activities you want, click **OK** to save the parallel activity template and close it. The parallel activity template then appears in **Templates** list.  

10. Repeat this procedure for a sequential activity, replacing instances of "parallel activity" with "sequential activity."  
