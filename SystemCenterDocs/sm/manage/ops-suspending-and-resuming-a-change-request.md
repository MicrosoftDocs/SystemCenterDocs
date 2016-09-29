---
title: Suspending and Resuming a Change Request
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
ms.assetid: f03242bf-a041-4388-8f94-e9d68e2eeb30
---

# Suspending and Resuming a Change Request

>Applies To: System Center 2016 - Service Manager

The procedures in this section describe how to suspend and resume a change request in Service Manager. Complete the following steps to suspend or resume a change request.  


## How to Put a Change Request on Hold

You can use the following procedures to put a change request on hold in Service Manager and then validate that the change request is on hold. For example, you might need to put a change request on hold if an external team needs to complete a manual activity.  

### To put a change request on hold  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Manual Activity In Progress**.  

3.  Select a change request to put on hold. For example, select **Apply Exchange Server Service Pack**.  

4.  In the **Tasks** pane, click **Put On Hold**.  

5.  In the **Comments** dialog box, type a note that indicates why the change request was put on hold, and then click **OK**.  

### To validate that the change request is on hold  

-   Click the **Change Requests: On Hold** view to ensure that the change request has been put on hold.  

## How to Resume a Change Request

You can use the following procedures to resume a change request that was put on hold in Service Manager and then validate that the change request was resumed. For example, you might need to resume a change request after an external team has completed a manual activity.  

### To resume a change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: On Hold**.  

3.  Select a change request. For example, select **Apply Exchange Server Updates**.  

4.  In the **Tasks** pane, click **Resume**.  

5.  In the **Comments** dialog box, type a comment, and then click **OK**.  

### To validate the change request was resumed  

-   If the current activity for a change request is a review activity, click the **Change Requests: In Review** view to ensure that the change request was resumed.  

-   If the current activity for a change request is a manual activity, click the **Change Requests: Manual Activity In Progress** view to ensure that the change request was resumed.  

## Optionally Unblock a Failed Change Request

You can use the following procedures to unblock a failed change request and then validate that the change request is unblocked. For example, you might need to unblock an activity of a change request that a review board or other review body has failed. Unblocking the change request resets the change request so that the change owner can provide more information.  

### To unblock a failed change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Failed**.  

3.  Select a change request. For example, select **Apply Exchange Server Service Pack**.  

4.  In the **Tasks** pane, click **Return To Activity**.  

5.  In the **Return to Activity** dialog box, select the failed activity, type a comment in the **Comments** box, and then click **OK**.  

### To validate the change request is unblocked  

-   If the failed activity for a change request is a review activity, click the **Change Requests: In Review** view to ensure that the change request is unblocked.  

-   If the failed activity for a change request is a manual activity, click the **Change Requests: Manual Activity In Progress** view to ensure that the change request is unblocked.  
