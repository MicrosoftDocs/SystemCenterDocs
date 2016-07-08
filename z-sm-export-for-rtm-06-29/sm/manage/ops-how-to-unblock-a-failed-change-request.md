---
title: How to Unblock a Failed Change Request
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b523841a-dac9-45c6-8d12-b4d66b2f31ae


















---
# How to Unblock a Failed Change Request
In System Center 2012 - Service Manager, you can use the following procedures to unblock a failed change request and then validate that the change request is unblocked. For example, you might need to unblock an activity of a change request that a review board or other review body has failed. Unblocking the change request resets the change request so that the change owner can provide more information.  
  
### To unblock a failed change request  
  
1.  In the Service Manager console, click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Failed**.  
  
3.  Select a change request. For example, select **Apply Exchange Server 2010 Service Pack 1**.  
  
4.  In the **Tasks** pane, click **Return To Activity**.  
  
5.  In the **Return to Activity** dialog box, select the failed activity, type a comment in the **Comments** box, and then click **OK**.  
  
### To validate the change request is unblocked  
  
-   If the failed activity for a change request is a review activity, click the **Change Requests: In Review** view to ensure that the change request is unblocked.  
  
-   If the failed activity for a change request is a manual activity, click the **Change Requests: Manual Activity In Progress** view to ensure that the change request is unblocked.  
  
## See Also  
 [Suspending and Resuming a Change Request](../../../sm/manage/operate/Suspending-and-Resuming-a-Change-Request.md)
