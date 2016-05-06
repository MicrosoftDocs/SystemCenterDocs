---
title: How to Create an Orchestrator Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c19dcf0d-85e7-43e7-a102-f40e7d46c1d6
robots: noindex,nofollow
---
# How to Create an Orchestrator Connector
You can use the following procedures in [!INCLUDE[smlong12](../Token/smlong12_md.md)] to create a connector for [!INCLUDE[orchlong](../Token/orchlong_md.md)] and then validate the creation of the connector.

### To create an [!INCLUDE[orchshort](../Token/orchshort_md.md)] connector

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Orchestrator connector**.

4.  Perform these steps to complete the [!INCLUDE[orchshort](../Token/orchshort_md.md)] Connector Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that **Enable this connector** is selected, and then click **Next**.

    3.  On the **Connection** page, in the **Server Information** area, type the URL of the Orchestrator Web service.

        1.  Type the URL of the Orchestrator Web service in the form of http:\/\/<computer>:<port>\/Orchestrator2012\/Orchestrator.svc, where <computer> is the name of the computer hosting the web service and <port> is the port number where the web service is installed. \(The default port number is 81.\)

    4.  On the **Connection** page, in the **Credentials** area, either select an existing account or click **New**, and then do the following:

        1.  In the **Run As Account** dialog box, in the **Display name** box, type a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to connect [!INCLUDE[orchshort](../Token/orchshort_md.md)], and then click **OK**. On the **Connection** page, click **Test Connection**.

            > [!NOTE]
            > Special characters \(such as the ampersand \[&\]\) in the **User Name** box are not supported.

        2.  In the **Test Connection** dialog box, make sure that the message “The connection to the server was successful” appears, and then click **OK**. On the **Connection** page, click **Next**.

    5.  On the **Folder** page, select a folder, and then click **Next**.

    6.  On the **Web Console URL** page, type the URL for the [!INCLUDE[orchshort](../Token/orchshort_md.md)] web console in the form of http:\/\/<computer>:port \(the default port number is 82\), and then click **Next**.

    7.  On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    8.  On the **Completion** page, make sure that you receive the message “Orchestrator connector successfully created,” and then click **Close**.

### To validate the creation of an [!INCLUDE[orchshort](../Token/orchshort_md.md)] connector

1.  In the **Connectors** pane, locate the [!INCLUDE[orchshort](../Token/orchshort_md.md)] connector that you created.

2.  Review the **Status** column for a status of **Finished Success**.

    > [!NOTE]
    > Allow sufficient time for the import process to finish if you are importing a large number of runbooks.

3.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Library**.

4.  In the **Library** pane, expand **Library**, and then click **Runbooks**.

5.  Review the **Runbooks** pane, and note that your runbooks have been imported.

