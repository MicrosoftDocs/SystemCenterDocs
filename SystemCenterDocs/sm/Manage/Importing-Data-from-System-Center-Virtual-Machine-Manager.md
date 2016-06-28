---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Importing Data from System Center Virtual Machine Manager
ms.technology:  service-manager
ms.assetid:  c43bfb32-0c1a-4e8e-8f10-373e68fc11a4
---

# Importing Data from System Center Virtual Machine Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

You can import objects, such as VM templates, service templates, and storage classifications that are created in Virtual Machine Manager (VMM) into the Service Manager database by creating a Virtual Machine Manager connector. After you import these objects into the Service Manager database, you can use these objects, for example, when you create Request Offerings.

If, in your environment, your VMM server pushes discovery data to an Operations Manager server, you will want to create an Operations Manager CI connector. You must make sure that the VMM management pack, Microsoft.SystemCenter.VirtualMachineManager.2016.Discovery, is synchronized with the Service Manager management server. You can create the Operations Manager CI connector either before or after creating the Virtual Machine Manager connector.

## How to Create a Virtual Machine Manager Connector

Use the following procedures to create a System Center Virtual Machine Manager connector and validate the creation of the connector.

### To create a System Center Virtual Machine Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Virtual Machine Manager connector**.

4.  Complete these steps to complete the Virtual Machine Manager Connector Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that **Enable this connector** is selected, and then click **Next**.

    3.  On the **Connection** page, in the **Server Information** area, type the same of the computer hosting Virtual Machine Manager (VMM).

    4.  On the **Connection** page, in the **Credentials** area, either select an existing account or click **New**, and then do the following:

        1.  In the **Run As Account** dialog box, in the **Display name** box, type a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to connect VMM, and then click **OK**. On the **Connection** page, click **Test Connection**.

            > [!NOTE]
            > Special characters (such as the ampersand [&]) in the **User Name** box are not supported.

        2.  In the **Test Connection** dialog box, make sure that **The connection to the server was successful** appears, and then click **OK**. On the **Connection** page, click **Next**.

    5.  On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    6.  On the **Completion** page, make sure that you receive a �Virtual Machine Manager connector successfully created� message, and then click **Close**.

### To validate the creation of a System Center Virtual Machine Manager connector

1.  In the **Connectors** pane, locate the System Center Virtual Machine Manager connector that you created.

2.  Review the **Status** column for a status of **Running**.

    > [!NOTE]
    > Allow sufficient time for the import process to finish if you are importing a large number of virtual machines or clouds.

3.  In the Service Manager console, click **Configuration Items**.

4.  In the **Tasks** pane, click **Create Folder**.

5.  In the Create New Folder Wizard, do the following:

    1.  In the **Folder name** box, type a name for the folder. For example, type **Test**.

    2.  In the **Management pack** area, make sure that an unsealed management pack of your choice is selected, and then click **OK**. For example, select **Service Catalog Generic Incident Request**.

6.  In the **Configuration Items** pane, click the folder you just created. For example, click **Test**.

7.  In the **Tasks** pane, click **Create View**.

8.  In the Create View Wizard, do the following:

    1.  On the **General** page, in the **Name** area, type a name for this view. For example, type **VMMTemplates**.

    2.  In the **Management pack** area, make sure that an unsealed management pack of your choice is selected. For example, select **Service Catalog Generic Incident Request**.

    3.  In the navigation pane of the wizard, click **Criteria**.

    4.  In the **Advanced Search** area, click **Browse**.

    5.  In the drop-down list (located to the right of the **Type to filter** box), select **All basic classes**.

    6.  In the **Type to filter** box, type **virtual machine template**, click **Virtual Machine Template**, click **OK**, and then click **OK** to save and close the form.

9. In the **Configuration Items** pane, expand the folder you created, and then click the view you created. For example, expand **Test**, and then click **VMMTemplates**

10. In the **VMMTemplates** pane, you will see the Virtual Machine Manager templates that have been created.



## How to Synchronize a Virtual Machine Manager Connector

To ensure that the Service Manager database is up to date, the Virtual Machine Manager connector synchronizes with Service Manager on a daily basis. You can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize a Virtual Machine Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Virtual Machine Manager connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

### To validate that a Virtual Machine Manager connector synchronized

1.  In the Service Manager console, click **Connectors**.

2.  In the **Connectors** pane, examine the start time and finish time to determine when the synchronization process started and finished.

    > [!NOTE]
    > Synchronization events are also written to the Event log in the Applications and Services Logs/Operations Manager folder.



## How to Disable and Enable a Virtual Machine Manager Connector
You can use the following procedures to disable or enable a Virtual Machine Manager connector and validate the status of the connector.

### To disable a virtual Machine Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Virtual Machine Manager connector that you want to disable.

4.  In the **Tasks** pane, under the connector name, click **Disable**.

5.  In the **Disable Connector** dialog box, click **OK**.

### To enable a virtual Machine Manager connector

1.  In the Service Manager console, click **Administration**, and then click **Connectors**.

2.  In the **Connectors** pane, select the Virtual Machine Manager connector that you want to enable.

3.  In the **Tasks** pane, under the connector name, click **Enable**.

4.  In the **Enable Connector** dialog box, click **OK**.

### To validate the status change of a virtual Machine Manager connector

1.  In the middle pane, locate the connector for which you have changed status, and then verify the value in the **Enabled** column.



