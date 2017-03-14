---
title: Choose changes to deploy
description: Explains how to choose changes to deploy in Service Manager.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e7ff2f4-4aca-4742-9401-e78f654a1d79
---

# Choose changes to deploy in Service Manager

>Applies To: System Center 2016 - Service Manager

The release manager selects approved changes for release by performing the following procedure. Using this process, the release manager links a manual activity in the release record to a dependent activity in a change request and then completes the manual activity in the release record. As a result, this process marks the dependent activity in the change request as completed.  

 The procedure to create a dependent activity to add it to a change request should already be completed before you proceed.

### To choose changes to deploy  

1.  In the Service Manager console, open the **Work Items** workspace, in the **Work Items** pane, expand **Release Management**, and then select **Release Management**.  

2.  In the **Work Items** pane, select a view under **Release Management** that displays a release record that comprises changes that are ready for deployment, and then double\-click the release record.  

3.  Click the **Activities** tab.  

4.  In the list that appears, right\-click a manual activity to link a change request dependent activity to, and then select **Link to Change Request Activity**.  

5.  In the **Select Change Request Activity** dialog box, select the change request to link to, expand it, and then select one or more dependent activities, and then click **OK** twice.  

    > [!TIP]  
    >  When you have linked the activity, the selected activity shows a linking indicator that resembles a chain icon. The tooltip for the selected activity shows IDs for the linked change request dependent activities.  

6.  Navigate to **Activity Management**, expand **Manual Activities**, and then select **In\-Progress Activities**.  

7.  Select the manual activity and then in the **Tasks** list click **Mark as Completed**.  

8.  Navigate to **Change Management**, expand **All Change Requests**, and then open the change request that is linked to the release record.  

9. Click the **Activities** tab and notice that the dependent activity is now marked **Completed**.  
