---
title: How to Synchronize an Orchestrator Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa9d1383-86cc-41e8-9752-9b2359b5c677
robots: noindex,nofollow
---
# How to Synchronize an Orchestrator Connector
To ensure that the Service Manager database in [!INCLUDE[smlong12](Token/smlong12_md.md)] is up to date, the [!INCLUDE[orchshort](Token/orchshort_md.md)] connector synchronizes with [!INCLUDE[sccore](Token/sccore_md.md)] on a daily basis. You can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize an [!INCLUDE[orchshort](Token/orchshort_md.md)] connector

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the [!INCLUDE[orchshort](Token/orchshort_md.md)] connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

### To validate that an [!INCLUDE[orchshort](Token/orchshort_md.md)] connector synchronized

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Connectors**.

2.  In the **Connectors** pane, examine the start time and finish time to determine when the synchronization process started and finished.

    > [!NOTE]
    > Synchronization events are also written to the Event log in the Applications and Services Logs\/Operations Manager folder.


