---
title: How to Create a Service Level Objective
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 703da8fd-217f-4cba-bb5c-56b7f06c34e1
---
# How to Create a Service Level Objective
In Service Manager, you create a service level objective to create relationships between a queue and a service level, a calendar item and a time metric, and actions that occur before or after service level breaches. Afterward, when you view incidents or service requests and they approach their warning time, you will see a notification bar stating that the item is about to breach. You can also create periodic notifications if you want analysts to receive email for incidents or service requests that might breach their service level objective. For more information about sending notifications, see [How to Send SLA Notification Information to the Assigned-To User](How-to-Send-SLA-Notification-Information-to-the-Assigned-To-User.md).

In order to create a service level objective, it is easier if you have already created or defined a calendar item and an SLA metric. Additionally, the service level objective that you create is linked to a queue. The queue that you associate to a service level objective must target the same type of work item, based on its class; otherwise, the queue will not be available when you create the service level objective.

### To create a service level objective

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Service Level Objective**.

3.  In the **Tasks** pane, under **Service Level Objectives**, click **Create Service Level Objective**.

4.  In the Create Service Level Objective Wizard, on the **Before You Begin** page, click **Next**.

5.  On the **General** page, in the **Title** box, type a name for the new service level objective.

6.  In the **Description** box, type a description of the service level objective.

7.  Next to **Class**, click **Browse** to Open the **Select a Class** dialog box and then select a class pertinent to the type of service level objective you are creating. Normally, you should choose either **Incident** or **Service Request**.

8.  Ensure that **Enabled** is selected, and then click **Next**.

9. On the **Service Level Criteria** page, select a calendar and a time metric, or you can create new ones. For more information about creating a calendar, see [How to Edit a Calendar Item](How-to-Edit-a-Calendar-Item.md). For more information about creating an SLA metric, see [How to Create SLA Metrics](How-to-Create-SLA-Metrics.md).

10. Under **Target**, specify the amount of time in hours or minutes that the work item should be completed by.

11. Under **Warning threshold**, specify the amount of time in hours or minutes before the service level is beached, which causes a warning notification in the work item notification bar, and then click **Next**.

12. On the **Summary** page confirm the choices you made, and then click **Create**.

13. On the **Completion** page, click **Close**.


