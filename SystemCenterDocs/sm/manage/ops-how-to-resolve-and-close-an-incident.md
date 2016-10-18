---
title: How to Resolve and Close an Incident
manager: cfreeman
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
ms.assetid: 411a309d-5233-4324-90e2-a4ba6b5ee644
---

# How to Resolve and Close an Incident

>Applies To: System Center 2016 - Service Manager

In Service Manager, you can use the following procedures to resolve and close an incident and then validate that the incident was resolved and closed.  

 After you research a problem and resolve its source, you can resolve and close the incident. An incident is considered resolved when the required change has been made. When the affected user has confirmed that the problem that caused the incident has been eliminated, the incident can be closed.  

### To resolve and close an incident  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Incident Management**, and then click **E\-Mail Incidents**.  

3.  In the **E\-Mail Incidents** view, select the incident you want to resolve and close.  

4.  In the **Tasks** pane, click **Change Incident Status** and then click **Resolve**.  

5.  In the **Resolve** dialog box, select the appropriate category for resolving this incident in the **Resolution Category** list. For example, select **Fixed by higher tier support**.  

6.  In the **Comments** box, type a comment that explains the resolution. For example, type **Resolved by installing Service Pack 1 on the Exchange server**, and then click **OK**.  

7.  In the **Tasks** pane, click **Change Incident Status** and then **Close**.  

8.  In the **Close** dialog box, type a comment about the closure of the incident, and then click **OK**.  

### To validate that an incident was resolved and closed  

-   In the **All Incidents** pane, the status for the incident or incidents changes from **Active** to **Resolved** when you resolve an incident and from **Resolved** to **Closed** when you close the incident.  

    > [!NOTE]  
    >  It might take a few seconds for the new status to appear. To immediately view the change, click **Refresh**.  
