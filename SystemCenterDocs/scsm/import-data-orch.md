---
title: Import Runbooks from System Center Orchestrator
description: Describes how you can import Runbooks from System Center Orchestrator into Service Manager.
manager: mkluck
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.prod: system-center
keywords:
ms.date: 05/12/2022
ms.technology: service-manager
ms.assetid: 33f8fa88-fad7-4354-bf6b-dbed1658ff0f
ms.custom: UpdateFrequency2
---

# Import Runbooks from System Center Orchestrator into Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

Service Manager integrates with Orchestrator, providing the capability to synchronously invoke runbooks from within Service Manager using workflows. This capability provides integration between Orchestrator automation capabilities with the Self-Service Portal and business modeling capabilities. When this capability is combined with the Service Manager Service Catalog stack, it's possible to create an end-user-facing request offering with an Orchestrator runbook as part of the fulfillment process.

Activities that make up a service request can be mapped to runbook activities, which in turn are mapped to an Orchestrator runbook. For example, the parameters that are necessary for a custom start activity to invoke a runbook in Orchestrator, such as a computer name, can go into as Service Manager as objects. You start this process by importing runbook objects into the Service Manager database using an Orchestrator connector. After you import runbooks into Service Manager, they appear in the **Library** node in the Administration workspace.

> [!NOTE]
> Ensure that you've installed the ADO.NET Data Services Update for .NET Framework 3.5 Service Pack 1 (SP1), as described in Microsoft Knowledge Base article 976127. For more information, see [ADO.NET Data Services Update](https://support.microsoft.com/topic/description-of-the-ado-net-data-services-update-for-net-framework-3-5-sp1-for-windows-server-2003-windows-xp-windows-vista-and-windows-server-2008-may-7-2010-e525c2b3-249c-7d66-3cb2-c029c786c745)

## Create an Orchestrator Connector

You can use the following procedures to create a connector for System Center - Orchestrator and then validate the creation of the connector.

### To create an Orchestrator connector

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Tasks** pane, under **Connectors**, select **Create Connector**, and select **Orchestrator connector**.

4. Perform these steps to complete the Orchestrator Connector Wizard:

   1. On the **Before You Begin** page, select **Next**.

   2. On the **General** page, in the **Name** box, enter a name for the new connector. Ensure that **Enable this connector** is selected, and select **Next**.

   3. On the **Connection** page, in the **Server Information** area, enter the URL of the Orchestrator Web service.
      ::: moniker range="sc-sm-2016"

      1. Enter the URL of the Orchestrator Web service in the form of http://computer:port/Orchestrator2012/Orchestrator.svc, where *computer* is the name of the computer hosting the web service and *port* is the port number where the web service is installed. (The default port number is 81.)
      ::: moniker-end

      ::: moniker range=">=sc-sm-1801"

      1. Enter the URL of the Orchestrator Web service in the form of http://computer:port/Orchestrator/Orchestrator.svc, where *computer* is the name of the computer hosting the web service and *port* is the port number where the web service is installed. (The default port number is 81.)
      ::: moniker-end

   4. On the **Connection** page, in the **Credentials** area, either select an existing account or select **New**, and then do the following:

      1.  In the **Run As Account** dialog, in the **Display name** box, enter a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to connect Orchestrator, and select **OK**. On the **Connection** page, select **Test Connection**.

          > [!NOTE]
          > Special characters (such as the ampersand [&]) in the **User Name** box aren't supported.

      2.  In the **Test Connection** dialog, ensure that the message *The connection to the server was successful* appears, and select **OK**. On the **Connection** page, select **Next**.

   5. On the **Folder** page, select a folder, and select **Next**.

   6. On the **Web Console URL** page, enter the URL for the Orchestrator web console in the form of http://computer:port (the default port number is 82), and select **Next**.

   7. On the **Summary** page, ensure that the settings are correct, and select **Create**.

   8. On the **Completion** page, ensure that you receive the message *Orchestrator connector successfully created*, and select **Close**.

### To validate the creation of an Orchestrator connector

1.  In the **Connectors** pane, locate the Orchestrator connector that you created.

2.  Review the **Status** column for a status of **Finished Success**.

    > [!NOTE]
    > Allow sufficient time for the import process to finish if you're importing a large number of runbooks.

3.  In the Service Manager console, select **Library**.

4.  In the **Library** pane, expand **Library**, and select **Runbooks**.

5.  Review the **Runbooks** pane, and note that your runbooks have been imported.




## Synchronize an Orchestrator connector

To ensure that the Service Manager database is up to date, the Orchestrator connector synchronizes with Service Manager on a daily basis. You can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize an Orchestrator connector

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Administration**, and select **Connectors**.

3.  In the **Connectors** pane, select the Orchestrator connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, select **Synchronize Now**.

### To validate that an Orchestrator connector synchronized

1.  In the Service Manager console, select **Connectors**.

2.  In the **Connectors** pane, examine the start time and finish time to determine when the synchronization process started and finished.

    > [!NOTE]
    > Synchronization events are also written to the Event log in the Applications and Services Logs/Operations Manager folder.


## Disable and enable an Orchestrator connector

You can use the following procedures to disable or enable an Orchestrator connector and validate the status of the connector.

### To disable an Orchestrator connector

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Administration**, and select **Connectors**.

3.  In the **Connectors** pane, select the Orchestrator connector that you want to disable.

4.  In the **Tasks** pane, under the connector name, select **Disable**.

5.  In the **Disable Connector** dialog, select **OK**.

### To enable an Orchestrator connector

1.  In the Service Manager console, select **Administration**, and select **Connectors**.

2.  In the **Connectors** pane, select the Orchestrator connector that you want to enable.

3.  In the **Tasks** pane, under the connector name, select **Enable**.

4.  In the **Enable Connector** dialog, select **OK**.

### To validate the status change of an Orchestrator connector

- In the middle pane, locate the connector for which you've changed status, and then verify the value in the **Enabled** column.

## Next steps

- Learn about how to [Import data from VMM](import-data-vmm.md).
