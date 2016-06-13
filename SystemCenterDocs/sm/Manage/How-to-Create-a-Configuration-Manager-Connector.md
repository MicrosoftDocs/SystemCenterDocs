---
title: How to Create a Configuration Manager Connector_1
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70db0991-63d5-464a-978b-45e8783ec539
---
# How to Create a Configuration Manager Connector_1
You can use the following procedures to create a connector to import data from Configuration Manager into [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] and confirm the status of the connector.

> [!IMPORTANT]
> Before you can create the Configuration Manager connector, you have to verify that System Center Configuration Manager is installed in your environment, and you have to turn on Windows User Account Control \(UAC\). For more information about UAC, see [User Account Control](http://go.microsoft.com/fwlink/p/?LinkID=177523).

### To create a Configuration Manager connector

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Configuration Manager Connector**. The System Center Configuration Manager Connector Wizard starts.

4.  On the **Before You Begin** page, click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Name** box, type a name for the new connector. For example, type **Configuration Manager Connector to Seattle**.

    2.  In the **Description** box, type a description for the new connector. For example, type **A Configuration Manager connector to site Seattle**.

    3.  Make sure that the **Enabled** check box is selected, and then click **Next**.

6.  On the **Select Management Pack** page, in the **Management Pack** list, select either **System Center Configuration Manager Connector Configuration** or **System Center Configuration Manager 2012 Connector Configuration**, and then click **Next**.

7.  On the **Connect to System Center Configuration Manager Database** page, do the following:

    1.  In the **Database Server Name** box, type the server name of the server that is hosting the System Center Configuration Manager site database and the database named instance, if applicable. For example, at the hypothetical Woodgrove Bank, you might type **woodgrove\\instance1** if the System Center Configuration Manager database is on a named instance of Microsoft SQL Server, or type **woodgrove** if the database is on a default instance of SQL Server.

    2.  In the **Database Name** box, type the name of the System Center Configuration Manager site database. For example, type **SMS\_CM1**.

    3.  In the **Credentials** area, select a Run As account, or create a new Run As account. The user account that you specify as the Run As account must be a member of the smsdbrole\_extract and the db\_datareader groups for the Configuration Manager site database.

    4.  In the **Credentials** area, click **Test Connection**.

    5.  In the **Credentials** dialog box, in the **Password** box, type the password for the account, and then click **OK**.

    6.  In the **Test Connection** dialog box, if you receive the following confirmation message, click **OK**:

        **The connection to the server was successful**.

    7.  Click **Next**.

8.  On the **Collections** page, select the appropriate collection, and then click **Next**.

9. On the **Schedule** page, in the **Synchronize** list, set the frequency and time of synchronization, and then click **Next**.

10. On the **Summary** page, confirm the connector settings you made, and then click **Create**.

11. On the **Confirmation** page, make sure that you receive the following confirmation message:

    “You have successfully completed the System Center Configuration Manager Connector Wizard.”

    Then, click **Close**.

    > [!NOTE]
    > The System Center Configuration Manager Connector Wizard may take several hours to import data from System Center Configuration Manager.

### To validate the creation of a Configuration Manager connector

1.  Confirm that the Configuration Manager connector that you created is displayed in the **Connectors** pane.

2.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Configuration Items**. In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**. Verify that the intended computers from  appear in the **All Windows Computers** pane.

3.  In the middle pane, double\-click a newly imported computer. Verify that the appropriate computer details appear in the computer form.

### To confirm the status of a Configuration Manager connector

-   View the columns in the **Connector** pane; the columns contain information about the start time, the finish time, the status, and the percentage of completion.

![](Image/PSSymbol.gif)You can use a Windows PowerShell command to create a new Configuration Manager 2007 connector. For information about how to use Windows PowerShell to create a new Configuration Manager 2007 connector in Service Manager, see [New\-SCCMConnector](http://go.microsoft.com/fwlink/p/?LinkId=225350).


