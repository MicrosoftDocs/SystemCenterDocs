---
title: How to Create a Queue
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b94a5c9-b426-4536-98b2-5fdc28455b80
robots: noindex,nofollow
---
# How to Create a Queue
You can create queues in [!INCLUDE[smlong12](Token/smlong12_md.md)] to create a grouping of related work items, such as incidents and change requests. For example, you can create a queue that you use for escalation, named **Exchange Send Problems Queue**, and then escalate that type of incident to that queue.

You can use the following procedure to create a queue.

### To create a queue

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Queues**.

3.  In the **Tasks** pane, click **Create Queue**.

4.  Complete these steps to complete the Create Queue Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, type a name in the **Queue name** box. For example, type **Exchange Send Problems Queue**.

    3.  Next to the **Work item type** box, click the ellipsis button \(**…**\). In the **Select a Class** dialog box, select a class, such as **Incident**, and then click **OK**.

    4.  In the **Management pack** list, select the unsealed management pack in which you want to store the new queue definition. For example, select **Service Manager Incident Management Configuration Library**. Then, click **Next**.

    5.  On the **Criteria** page, build the criteria that you want to use to filter work items for the queue, and then click **Next**. Only work items that meet the specified criteria will be added to that queue.

        For example, select the **Classification Category** property in the **Available Properties** area, and then click **Add**. In the list that was just added to the **Criteria** area, in the area that is now surrounded by a red box, select **E\-Mail Problems**, and then click **Next**.

    6.  On the **Summary** page, click **Create** to create the queue.

    7.  On the **Completion** page, click **Close**.

### To validate the creation of a queue

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], verify that the new queue appears in the **Queues** pane.

2.  In the **Tasks** pane, click **Properties**, and then verify that the queue appears as you defined it.

![](Image/PSSymbol.gif)You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to retrieve queues that are defined in [!INCLUDE[smshort](Token/smshort_md.md)], see [Get\-SCSMQueue](http://go.microsoft.com/fwlink/p/?LinkId=225331).


