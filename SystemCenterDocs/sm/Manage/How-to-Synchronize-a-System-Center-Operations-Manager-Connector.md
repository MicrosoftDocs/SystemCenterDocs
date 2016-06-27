---
title: How to Synchronize a System Center Operations Manager Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2696dbca-8160-471e-8b10-e678a25329cc
---
# How to Synchronize a System Center Operations Manager Connector

>Applies To: System Center 2016 Technical Preview - Service Manager

When you create a System Center Operations Manager alert connector for Service Manager, it polls Operations Manager every 30 seconds. When you create an Operations Manager configuration item (CI) connector, it synchronizes data from Operations Manager every day at the time you specified in the configured schedule. However, you can use the following procedure to manually synchronize either type of connector.

> [!NOTE]
> The **Start Time** and **Finish Time** values are not updated when an alert connector is synchronized. These values are only updated when alert data is transferred between Operations Manager and Service Manager.

### To manually synchronize an Operations Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to synchronize.

4.  In the **Tasks** pane, under the connector name, click **Synchronize Now**.

5.  In the **Synchronize Now** dialog box, click **OK**.

### To validate Operations Manager connector synchronization

1.  In the Service Manager console, click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Computers**, and then click **All Windows Computers**. Verify that any new computers that were discovered in Operations Manager appear in the **All Windows Computers** pane.



