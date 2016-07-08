---
title: How to Add a Change Reviewer
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a99893e3-d65e-4ae1-8961-b143611296b5


















---
# How to Add a Change Reviewer
In System Center 2012 - Service Manager, you can use the following procedures to add a change reviewer for an existing change request and then validate that the reviewer was added. You can select who reviews change requests in a way that supports your business processes. For example, if a change affects a process for which certain people are responsible, you can give those people the ability to approve change requests that affect the process.  
  
### To add a change reviewer  
  
1.  In the Service Manager console, click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Work Items**, click **Change Management**, and then click **All Change Requests**.  
  
3.  Double\-click a change request to open it. For example, double\-click **Apply Exchange Server 2010 Service Pack 1**.  
  
4.  Click the **Activities** tab to view the list of manual and review activities.  
  
5.  Double\-click the activity to which you want to add a reviewer. The activity must have a status of **In Progress** or **Pending**, and in the ID column, the activity must also have the **RA** prefix or the prefix you defined for review activities.  
  
6.  In the dialog box that appears, click **Add**, type the name of a reviewer, select **Must Vote**, and then click **OK**. For example, type **Aaron Lee**.  
  
7.  Click **OK** to close the dialog box, and then click **OK** to update the change request and to close the form.  
  
### To validate that a reviewer was added  
  
1.  Double\-click the change request to which you added a reviewer. For example, double\-click **Apply Exchange Server 2010 Service Pack 1**.  
  
2.  Click the **Activities** tab, and then double\-click the activity to which you added a reviewer.  
  
3.  Verify that the reviewer was added.  
  
## See Also  
 [Approving and Modifying Change Requests](../../../sm/manage/operate/Approving-and-Modifying-Change-Requests.md)
