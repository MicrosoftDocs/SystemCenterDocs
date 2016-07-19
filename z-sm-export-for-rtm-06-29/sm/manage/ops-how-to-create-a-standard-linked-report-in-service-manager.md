---
title: How to Create a Standard Linked Report in Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e91869e2-981b-4f62-866e-ac51e495cf05


















---
# How to Create a Standard Linked Report in Service Manager
You can use the following procedure in System Center 2012 - Service Manager to create a linked report.  
  
 A linked report is a shortcut to a report—it is similar to a program shortcut on your desktop. A linked report is derived from publicly defined reports from any management pack. A linked report retains some of the original report's properties, such as the report layout. Other properties of the linked report, such as parameters and subscriptions, can be different from the original report.  
  
### To create a linked report  
  
1.  In the **Reporting** view, select the report you want to use as the basis for the linked report, and then, in the **Tasks** pane, click **Run Report**.  
  
2.  In the **Report** window, click **Save as Linked Report** in the **Task** pane.  
  
3.  Type a name and an optional description for the new linked report.  
  
4.  Select a management pack for the linked report.  
  
5.  Click **Select Folder**, and then select the folder in which you want to save the report.  
  
6.  Click **OK**.  
  
7.  Close the report.  
  
 After the next data warehouse synchronization, the new linked report is displayed in the folder where you saved it. For information about scheduling a data warehouse synchronization job, see [How to Schedule a Data Warehouse Job](http://go.microsoft.com/fwlink/p/?LinkId=229828).  
  
> [!NOTE]  
>  You might have to close and reopen the console after the synchronization job is complete to see the report.  
  
## See Also  
 [Using and Managing Standard Reports](../../../sm/manage/operate/Using-and-Managing-Standard-Reports.md)
