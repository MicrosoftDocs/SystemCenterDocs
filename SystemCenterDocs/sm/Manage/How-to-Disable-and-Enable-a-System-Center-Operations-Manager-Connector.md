---
title: How to Disable and Enable a System Center Operations Manager Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5dadc67-53a9-4b38-bdb8-eaf78e2d23aa
---
# How to Disable and Enable a System Center Operations Manager Connector
You can use the following procedures to disable or enable a System Center Operations Manager connector for Service Manager and validate the changes.

For example, after you configure an Operations Manager connector, if you must perform maintenance operations on the [!INCLUDE[smshort](../../includes/smshort_md.md)] database, you can temporarily disable the connector and suspend the data import. You can resume the data import by re\-enabling the connector.

For more information about how to delete a product connector from System Center Operations Manager, see [Removing an Old Product Connector](http://go.microsoft.com/fwlink/?LinkId=188974) on Kevin Holman’s System Center blog.

### To disable an Operations Manager connector

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to disable.

4.  In the **Tasks** pane, under the connector name, click **Disable**.

5.  In the **Disable Connector** dialog box, click **OK**.

### To enable an Operations Manager connector

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to enable.

4.  In the **Tasks** pane, under the connector name, click **Enable**.

5.  In the **Enable Connector** dialog box, click **OK**.

### To validate the status change of an Operations Manager connector

1.  Wait 30 seconds. Then, in the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**, and then click **Connectors**.

2.  In the **Connectors** pane, locate the connector for which you have changed the status, and verify the value in the **Enabled** column.

![](../../media/PSSymbol.gif)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to start a Service Manager connector, see [Start\-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkId=225378).

-   For information about how to use Windows PowerShell to retrieve connectors that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)] and view their status, see [Get\-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkId=225320).

-   For information about how to use Windows PowerShell to update the properties of a [!INCLUDE[smshort](../../includes/smshort_md.md)] connector, see [Update\-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225382).


