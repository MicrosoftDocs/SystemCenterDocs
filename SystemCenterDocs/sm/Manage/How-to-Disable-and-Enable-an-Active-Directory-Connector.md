---
title: How to Disable and Enable an Active Directory Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c30e2c5e-2381-448b-a9ec-314c76a65ae5
---
# How to Disable and Enable an Active Directory Connector
You can use the following procedure to disable or enable an Active Directory connector in Service Manager and validate its change in status.

### To disable an Active Directory connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Active Directory connector that you want to disable.

4.  In the **Tasks** pane, under the connector name, click **Disable**.

5.  In the **Disable Connector** dialog box, click **OK**.

### To enable an Active Directory connector

1.  In the Service Manager console, click **Administration**, and then click **Connectors**.

2.  In the **Connectors** pane, select the Active Directory connector that you want to enable.

3.  In the **Tasks** pane, under the connector name, click **Enable**.

4.  In the **Enable Connector** dialog box, click **OK**.

### To validate the status change of an Active Directory connector

1.  After you enable or disable an Active Directory connector, wait for about 30 seconds. Then, in the Service Manager console, click **Administration**, and then click **Connectors**.

2.  In the middle pane, locate the connector for which you have changed status, and then verify the value in the **Enabled** column.

![](../../media/pssymbol.png)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to start a Service Manager connector, see [Start\-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225378).

-   For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and view their status, see [Get\-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225320).

-   For information about how to use Windows PowerShell to update properties of a Service Manager connector, see [Update\-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225382).


