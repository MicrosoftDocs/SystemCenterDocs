---
title: How to Create a Release Record Template
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
ms.assetid: 14145889-abbe-4549-8bc8-89a1964b3587
---

# How to Create a Release Record Template

>Applies To: System Center 2016 - Service Manager

A release record template is used to create new release records. A release record template can include predefined release activities. When you use a template for new release records, new release records are created faster than when you create them from scratch.  

 The template author creates a template for release records by completing the following procedure.  

### To create a release record template  

1.  In the Service Manager console, open the **Library** workspace, and in the **Library** pane, select **Templates**.  

2.  In the **Templates** list, select **Default Release Record**, and then in the **Tasks** pane under **Templates**, click **Create Template**.  

3.  In the **Create Template** dialog box, type a name for the template and a description of what the template applies.  

4.  Under **Class**, click **Browse**, and in the **Select a Class** box, select **Release Record**, and then click **OK** to close the **Select a Class** box.  

5.  Click **OK** to close the **Create Template** dialog box, and the New Release Record Template form appears.  

6.  Enter information in the boxes on the **General** tab, and then click the **Activities** tab.  

7.  You can add, delete, or modify sets of activities to the release record template, including the following actions:  

    -   Add activities from the list of existing activity templates.  

    -   Move activities up and down in the order in which they are completed.  

    -   Move activities in the process list, and place them inside container activities.  

    -   Move activities from container activities, and place them anywhere in the process list.  

    -   Delete activities.  

8.  As you add an activity, the activity form opens. Enter necessary information, and then click **OK** to save the activity.  

9. When you have added all the activities you want, click **OK** to save the release record template and close it. The release record template then appears in **Templates** list.  
