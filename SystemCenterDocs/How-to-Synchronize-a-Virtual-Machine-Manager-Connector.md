---
title: How to Synchronize a Virtual Machine Manager Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7998989-0584-4b24-bf1f-3f53a0cd6aa5
robots: noindex,nofollow
---
# How to Synchronize a Virtual Machine Manager Connector
To ensure that the [!INCLUDE[smshort](./Token/smshort_md.md)] database is up to date, the Virtual Machine Manager connector synchronizes with [!INCLUDE[sccore](./Token/sccore_md.md)] on a daily basis. You can use the following procedures in [!INCLUDE[smlong12](./Token/smlong12_md.md)] to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize a Virtual Machine Manager connector

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Virtual Machine Manager connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

### To validate that a Virtual Machine Manager connector synchronized

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Connectors**.

2.  In the **Connectors** pane, examine the start time and finish time to determine when the synchronization process started and finished.

    > [!NOTE]
    > Synchronization events are also written to the Event log in the Applications and Services Logs\/Operations Manager folder.


