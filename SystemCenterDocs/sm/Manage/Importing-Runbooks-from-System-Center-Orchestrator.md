---
title: Importing Runbooks from System Center Orchestrator
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33f8fa88-fad7-4354-bf6b-dbed1658ff0f
---
# Importing Runbooks from System Center Orchestrator
Service Manager integrates with Orchestrator, providing the capability to synchronously invoke runbooks from within Service Manager through the use of workflows. This capability provides integration between Orchestrator automation capabilities with the Self\-Service Portal, as well as business modeling capabilities. When this capability is combined with the Service Manager Service Catalog stack, it is possible to create an end\-user\-facing request offering with an Orchestrator runbook as part of the fulfillment process.

Activities that make up a service request can be mapped to runbook activities, which in turn are mapped to an Orchestrator runbook. For example, the parameters that are necessary for a custom start activity to invoke a runbook in Orchestrator, such as a computer name, can go into as Service Manager as objects. You start this process by importing runbook objects into the Service Manager database using an Orchestrator connector. After you import runbooks into Service Manager, they appear in the **Library** node in the Administration workspace.

> [!NOTE]
> Make sure that you have installed the ADO.NET Data Services Update for .NET Framework 3.5 Service Pack 1 \(SP1\), as described in Microsoft Knowledge Base article 976127. For more information, see [ADO.NET Data Services Update](http://go.microsoft.com/fwlink/p/?LinkID=224398).

## How to Create an Orchestrator Connector

You can use the following procedures to create a connector for System Center 2012 \- Orchestrator and then validate the creation of the connector.

### To create an Orchestrator connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Orchestrator connector**.

4.  Perform these steps to complete the Orchestrator Connector Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that **Enable this connector** is selected, and then click **Next**.

    3.  On the **Connection** page, in the **Server Information** area, type the URL of the Orchestrator Web service.

        1.  Type the URL of the Orchestrator Web service in the form of http:\/\/\<computer\>:\<port\>\/Orchestrator2012\/Orchestrator.svc, where \<computer\> is the name of the computer hosting the web service and \<port\> is the port number where the web service is installed. \(The default port number is 81.\)

    4.  On the **Connection** page, in the **Credentials** area, either select an existing account or click **New**, and then do the following:

        1.  In the **Run As Account** dialog box, in the **Display name** box, type a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to connect Orchestrator, and then click **OK**. On the **Connection** page, click **Test Connection**.

            > [!NOTE]
            > Special characters \(such as the ampersand \[&\]\) in the **User Name** box are not supported.

        2.  In the **Test Connection** dialog box, make sure that the message “The connection to the server was successful” appears, and then click **OK**. On the **Connection** page, click **Next**.

    5.  On the **Folder** page, select a folder, and then click **Next**.

    6.  On the **Web Console URL** page, type the URL for the Orchestrator web console in the form of http:\/\/\<computer\>:port \(the default port number is 82\), and then click **Next**.

    7.  On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    8.  On the **Completion** page, make sure that you receive the message “Orchestrator connector successfully created,” and then click **Close**.

### To validate the creation of an Orchestrator connector

1.  In the **Connectors** pane, locate the Orchestrator connector that you created.

2.  Review the **Status** column for a status of **Finished Success**.

    > [!NOTE]
    > Allow sufficient time for the import process to finish if you are importing a large number of runbooks.

3.  In the Service Manager console, click **Library**.

4.  In the **Library** pane, expand **Library**, and then click **Runbooks**.

5.  Review the **Runbooks** pane, and note that your runbooks have been imported.




## How to Synchronize an Orchestrator Connector

To ensure that the Service Manager database is up to date, the Orchestrator connector synchronizes with Service Manager on a daily basis. You can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize an Orchestrator connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Orchestrator connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

### To validate that an Orchestrator connector synchronized

1.  In the Service Manager console, click **Connectors**.

2.  In the **Connectors** pane, examine the start time and finish time to determine when the synchronization process started and finished.

    > [!NOTE]
    > Synchronization events are also written to the Event log in the Applications and Services Logs\/Operations Manager folder.



## How to Disable and Enable an Orchestrator Connector

You can use the following procedures to disable or enable an Orchestrator connector and validate the status of the connector.

### To disable an Orchestrator connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Orchestrator connector that you want to disable.

4.  In the **Tasks** pane, under the connector name, click **Disable**.

5.  In the **Disable Connector** dialog box, click **OK**.

### To enable an Orchestrator connector

1.  In the Service Manager console, click **Administration**, and then click **Connectors**.

2.  In the **Connectors** pane, select the Orchestrator connector that you want to enable.

3.  In the **Tasks** pane, under the connector name, click **Enable**.

4.  In the **Enable Connector** dialog box, click **OK**.

### To validate the status change of an Orchestrator connector

- In the middle pane, locate the connector for which you have changed status, and then verify the value in the **Enabled** column.


