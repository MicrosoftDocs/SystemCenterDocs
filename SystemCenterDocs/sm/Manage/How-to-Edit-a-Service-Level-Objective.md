---
title: How to Edit a Service Level Objective
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: af23bd77-699a-48b7-91e2-fc1273c5edd2
---
# How to Edit a Service Level Objective
In Service Manager, you can edit a service level objective to modify relationships between a queue and a service level, a calendar item and a time metric, and actions that occur before or after service level breaches. Afterward, when you view incidents or service requests and they approach their warning time, you will see a notification bar stating that the item is about to breach. You can also create periodic notifications if you want analysts to receive email for incidents or service requests that might breach their service level objective.

The service level objective that you edit is linked to a queue. If you want to modify the association of queue to a service level objective, the service level objective must target the same type of work item as the queue, based on its class; otherwise, the queue will not be available when you modify the service level objective.

### To modify a service level objective

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Service Level Objective**.

3.  In the **Service Level Objectives** list, select an existing service level objective, and then in the **Tasks** pane, under **\<ServiceLevelObjectiveName\>**, click **Properties**.

4.  In the **Edit SLO** dialog box, modify any of the following items, as needed. For more information about the elements on this page, see [How to Create a Service Level Objective](How-to-Create-a-Service-Level-Objective.md).

    -   **Title**

    -   **Queues**

    -   **Service Level Criteria**

5.  Click **OK** to close the **Edit SLO** dialog box.


