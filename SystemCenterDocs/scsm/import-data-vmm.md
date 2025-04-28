---
title: Import Data from Virtual Machine Manager
description: Describes how you can import data from Virtual Machine Manager into Service Manager.
ms.topic: how-to
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.service: system-center
keywords:
ms.date: 04/28/2025
ms.subservice: service-manager
ms.assetid: c43bfb32-0c1a-4e8e-8f10-373e68fc11a4
ms.custom: UpdateFrequency3, engagement-fy24
---

# Import data from Virtual Machine Manager into Service Manager

This article describes how you can import data from Virtual Machine Manager into Service Manager.

You can import objects, such as VM templates, service templates, and storage classifications that are created in Virtual Machine Manager (VMM) into the Service Manager database by creating a Virtual Machine Manager connector. After you import these objects into the Service Manager database, you can use these objects, for example, when you create Request Offerings.

If, in your environment, your VMM server pushes discovery data to an Operations Manager server, you'll want to create an Operations Manager CI connector. You must ensure that the VMM management pack, Microsoft.SystemCenter.VirtualMachineManager.\<version\>.Discovery, is synchronized with the Service Manager management server. You can create the Operations Manager CI connector either before or after creating the Virtual Machine Manager connector.

## Create a Virtual Machine Manager connector

Use the following procedures to create a System Center Virtual Machine Manager connector and validate the creation of the connector.

To create a System Center Virtual Machine Manager connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Tasks** pane, under **Connectors**, select **Create Connector**, and select **Virtual Machine Manager connector**.

4. Complete these steps to complete the Virtual Machine Manager Connector Wizard:

    1. On the **Before You Begin** page, select **Next**.

    2. On the **General** page, in the **Name** box, enter a name for the new connector. Ensure that **Enable this connector** is selected, and select **Next**.

    3. On the **Connection** page, in the **Server Information** area, enter the same of the computer hosting Virtual Machine Manager (VMM).

    4. On the **Connection** page, in the **Credentials** area, either select an existing account or select **New**, and then do the following:

        1. In the **Run As Account** dialog, in the **Display name** box, enter a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to connect VMM, and select **OK**. On the **Connection** page, select **Test Connection**.

            > [!NOTE]
            > Special characters (such as the ampersand [&]) in the **User Name** box aren't supported.

        2. In the **Test Connection** dialog, ensure that **The connection to the server was successful** appears, and select **OK**. On the **Connection** page, select **Next**.

    5. On the **Summary** page, ensure that the settings are correct, and select **Create**.

    6. On the **Completion** page, ensure that you receive a *Virtual Machine Manager connector successfully created* message, and select **Close**.

### Validate the creation of a System Center Virtual Machine Manager connector

To validate the creation of an SCVMM connector, follow these steps:

1. In the **Connectors** pane, locate the System Center Virtual Machine Manager connector that you created.

2. Review the **Status** column for a status of **Running**.

    > [!NOTE]
    > Allow sufficient time for the import process to finish if you're importing a large number of virtual machines or clouds.

3. In the Service Manager console, select **Configuration Items**.

4. In the **Tasks** pane, select **Create Folder**.

5. In the Create New Folder Wizard, do the following:

    1. In the **Folder name** box, enter a name for the folder. For example, enter **Test**.

    2. In the **Management pack** area, ensure that an unsealed management pack of your choice is selected, and select **OK**. For example, select **Service Catalog Generic Incident Request**.

6. In the **Configuration Items** pane, select the folder you just created. For example, select **Test**.

7. In the **Tasks** pane, select **Create View**.

8. In the Create View Wizard, do the following:

    1. On the **General** page, in the **Name** area, enter a name for this view. For example, enter **VMMTemplates**.

    2. In the **Management pack** area, ensure that an unsealed management pack of your choice is selected. For example, select **Service Catalog Generic Incident Request**.

    3. In the navigation pane of the wizard, select **Criteria**.

    4. In the **Advanced Search** area, select **Browse**.

    5. In the dropdown list (located to the right of the **Type to filter** box), select **All basic classes**.

    6. In the **Type to filter** box, enter **virtual machine template**, select **Virtual Machine Template**, select **OK**, and select **OK** to save and close the form.

9. In the **Configuration Items** pane, expand the folder you created, and select the view you created. For example, expand **Test**, and select **VMMTemplates**

10. In the **VMMTemplates** pane, you'll see the Virtual Machine Manager templates that have been created.

## Synchronize a Virtual Machine Manager connector

To ensure that the Service Manager database is up to date, the Virtual Machine Manager connector synchronizes with Service Manager on a daily basis. You can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### Manually synchronize a Virtual Machine Manager connector

To manually synchronize a VMM connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Virtual Machine Manager connector that you want to synchronize.

4. In the **Tasks** pane, under the name of the connector, select **Synchronize Now**.

### Validate the synchronization of a Virtual Machine Manager connector

To validate that a VMM connector is synchronized, follow these steps:

1. In the Service Manager console, select **Connectors**.

2. In the **Connectors** pane, examine the start time and finish time to determine when the synchronization process started and finished.

    > [!NOTE]
    > Synchronization events are also written to the Event log in the Applications and Services Logs/Operations Manager folder.

## Disable and enable a Virtual Machine Manager connector

You can use the following procedures to disable or enable a Virtual Machine Manager connector and validate the status of the connector.

### [Disable a virtual Machine Manager connector](#tab/disable-a-virtual-machine-manager-connector)

To disable a VMM connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Virtual Machine Manager connector that you want to disable.

4. In the **Tasks** pane, under the connector name, select **Disable**.

5. In the **Disable Connector** dialog, select **OK**.

### [Enable a virtual Machine Manager connector](#tab/enable-a-virtual-machine-manager-connector)

To enable a VMM connector, follow these steps:

1. In the Service Manager console, select **Administration**, and select **Connectors**.

2. In the **Connectors** pane, select the Virtual Machine Manager connector that you want to enable.

3. In the **Tasks** pane, under the connector name, select **Enable**.

4. In the **Enable Connector** dialog, select **OK**.

### [Validate the status change of a virtual Machine Manager connector](#tab/validate-the-status-change-of-a-virtual-machine-manager-connector)

To validate the status change of a VMM connector, follow this step:

In the middle pane, locate the connector for which you've changed status, and then verify the value in the **Enabled** column.

---

## Next steps

Review the [Configuration items](config-items.md) article to learn about storing information about services, computers, software, software updates, users, and other undefined imported objects in the Service Manager database.
