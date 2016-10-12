---
title: Step 8 - Create a New View
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
ms.assetid: 67929ae2-57a4-4810-a34a-ab73d66287c5
---

# Step 8 - Create a New View

>Applies To: System Center 2016 - Service Manager

To continue with the customizations in the Woodgrove Bank scenario, in this step Ken creates the **Compliance Change Requests** view that will display only change requests of the **Compliance** type. Ken saves the new view to the **Service Manager Change Management Configuration Library** management pack. Users can monitor these change requests in the Service Manager console.  

### Create a new view  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Change Management**.  

3.  In the **Tasks** pane, click **Create View**.  

4.  In the **General** section of the **Create View** dialog box, type **Compliance Change Requests** in the **Name** box.  

5.  Select the **Criteria** section.  

6.  Next to the **Search for objects of a specific class** list, click **Browse**.  

7.  In the **Select a Class** dialog box, under **Name**, select **Change Request**. In the **Available Properties** list select **Area**, and then click **Add**.  

8.  At the end of the **Criteria** section, in the **Criteria** definition area, select the **Area** criterion, and in the empty box, set the value to **Compliance**. When the criterion is complete, it resembles **\[Change Request\] Area equals Compliance**.  

9. Click **Display**, and in the **Columns to display** list, select **Status**, **Classification Category**, and **Description**. Then, click **OK**.  
