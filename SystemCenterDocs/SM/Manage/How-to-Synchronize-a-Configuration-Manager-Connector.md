---
title: How to Synchronize a Configuration Manager Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d92b95a-0db7-43df-95ce-2732f54df3c1
---
# How to Synchronize a Configuration Manager Connector
To ensure that the Service Manager database is up to date, the System Center Configuration Manager connector synchronizes with Configuration Manager every day after the initial synchronization. However, you can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize a Configuration Manager connector

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Configuration Manager connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

    > [!NOTE]
    > Depending on the amount of data that is imported, you might have to wait for the import to be completed.

### To validate that a Configuration Manager connector synchronized

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Computers**, and then click **All Windows Computers**. Verify that any new computers in Configuration Manager appear in the middle pane.


