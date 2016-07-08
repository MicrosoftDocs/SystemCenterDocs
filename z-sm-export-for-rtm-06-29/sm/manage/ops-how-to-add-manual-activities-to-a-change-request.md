---
title: How to Add Manual Activities to a Change Request
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1182c49-0c65-4d93-a8b1-b309d5940bcc


















---
# How to Add Manual Activities to a Change Request
In System Center 2012 - Service Manager, you can use the following procedures to add a manual activity and then assign it to yourself and then validate that the manual activity was added. For example, when you investigate a new change request, you might want to add a manual activity to the change request. This manual activity could be any task that is not defined in the change request template that was used to create the change request.  
  
> [!NOTE]  
>  You cannot delete an activity in a change request if the change request is in progress, however you can skip the activity or put the change request on hold and then delete the activity.  
  
### To add a manual activity  
  
1.  In the Service Manager console, click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  
  
3.  Double\-click the change request to which you want to add a manual activity. For example, double\-click **Apply Exchange Server 2010 Service Pack 1**.  
  
4.  Click the **Activities** tab, and then click **Add**. In the **Select Template** dialog box, click **Default Manual Activity**, and then click **OK**.  
  
5.  In the **Title** box, type a name that describes the manual activity. For example, type **Warranty Review**.  
  
6.  In the **Description** box, type a description of the manual activity. For example, type **Verify that the server is still under warranty before approval**.  
  
7.  Under **Activity Implementer**, click the ellipsis button \(…\).  
  
8.  In the **Select User** dialog box, select the name of the person who will perform the manual activity, and then click **OK**. For example, select **Aaron Lee**.  
  
9. Click **OK** to update the changes to the manual activity.  
  
10. Click **OK** to update the change request and to close the form.  
  
### To validate that the manual activity was added  
  
-   Reopen the change request, and then click the **Activities** tab to view the manual activity that you added.  
  
## See Also  
 [Initiating and Classifying a Change Request](../../../sm/manage/operate/Initiating-and-Classifying-a-Change-Request.md)
