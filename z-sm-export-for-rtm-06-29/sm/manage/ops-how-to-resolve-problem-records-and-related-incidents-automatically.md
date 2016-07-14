---
title: How to Resolve Problem Records and Related Incidents Automatically
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1030f50e-38dc-4892-9092-e2e439ed01f3


















---
# How to Resolve Problem Records and Related Incidents Automatically
In System Center 2012 - Service Manager, you can use the following procedures to resolve a problem record and the incidents that are associated with it and then validate the resolution.  
  
### To resolve a problem record and the incidents that are associated with it  
  
1.  In the Service Manager console, click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  
  
3.  In the **Active Problems** view, double\-click the problem record that you want to resolve. Then, in the **Tasks** pane, click **Resolve**.  
  
4.  Click the **Resolution** tab, and then click to select the **Auto\-resolve all incidents associated with this problem** check box.  
  
5.  In the **Resolution Category** box, select the appropriate category.  
  
6.  In the **Resolution Description** box, type a summary of the resolution for this problem record. For example, type **Application of Exchange Server 2010 SP1 fixed the restricted permission problem that affected users across forests**.  
  
7.  Click **OK**.  
  
### To validate problem and incident resolution  
  
-   Verify that the incidents associated with the problem record appear in the **All Incidents** view and that they have a status of **Resolved**.  
  
    > [!NOTE]  
    >  It might take a few minutes for the incident status to be updated to **Resolved**.  
  
## See Also  
 [Managing Problems](../../../sm/manage/operate/Managing-Problems.md)
