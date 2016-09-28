---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Disable and Enable a Configuration Manager Connector
ms.technology:  service-manager
ms.assetid:  bf2d8feb-76ce-40b8-a3c6-41d6aac284ea
---

# How to Disable and Enable a Configuration Manager Connector

>Applies To: System Center 2016 - Service Manager

You can use the following procedures to disable or enable a System Center Configuration Manager connector and validate the status of the change.

### To disable a Configuration Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Configuration Manager connector that you want to disable. For example, click **Configuration Manager connector to SEA**.

4.  In the **Tasks** pane, under the connector name, click **Disable**.

    > [!NOTE]
    > If you disable a connector while it is synchronizing data, the synchronization process may not stop. However, a disabled connector will not import any new data from a Configuration Manager database from that point forward.

### To enable a Configuration Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Configuration Manager connector that you want to enable. For example, click **Configuration Manager connector to SEA**.

4.  In the **Tasks** pane, under the connector name, click **Enable**.

### To validate the status change of a Configuration Manager connector

1.  After you disable or enable the connector, wait 30 seconds. Then, in the Service Manager console, click **Administration**, and then click **Connectors**.

2.  In the **Connectors** pane, locate the connector for which you have changed status, and verify the value in the **Enabled** column.

3.  If you enabled the connector, verify that the connector resumes synchronization according to the schedule. If you disabled the connector, verify that the connector no longer synchronizes according to the schedule.

![PowerShell symbol](../media/pssymbol.png)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to start a Service Manager connector, see [Start-SCSMConnector](http://go.microsoft.com/fwlink/?LinkId=203113).

-   For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and view their status, see [Get-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkId=225320).

-   For information about how to use Windows PowerShell to update the properties of a Service Manager connector, see [Update-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225382).
