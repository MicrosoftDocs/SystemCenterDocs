---
title: Step 8: Create a New View
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67929ae2-57a4-4810-a34a-ab73d66287c5
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
# Step 8: Create a New View
To continue with the customizations in the Woodgrove Bank scenario, in this step Ken creates the **Compliance Change Requests** view that will display only change requests of the **Compliance** type. Ken saves the new view to the **Service Manager Change Management Configuration Library** management pack. Users can monitor these change requests in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
### Create a new view  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Change Management**.  
  
3.  In the **Tasks** pane, click **Create View**.  
  
4.  In the **General** section of the **Create View** dialog box, type **Compliance Change Requests** in the **Name** box.  
  
5.  Select the **Criteria** section.  
  
6.  Next to the **Search for objects of a specific class** list, click **Browse**.  
  
7.  In the **Select a Class** dialog box, under **Name**, select **Change Request**. In the **Available Properties** list select **Area**, and then click **Add**.  
  
8.  At the end of the **Criteria** section, in the **Criteria** definition area, select the **Area** criterion, and in the empty box, set the value to **Compliance**. When the criterion is complete, it resembles **\[Change Request\] Area equals Compliance**.  
  
9. Click **Display**, and in the **Columns to display** list, select **Status**, **Classification Category**, and **Description**. Then, click **OK**.  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)