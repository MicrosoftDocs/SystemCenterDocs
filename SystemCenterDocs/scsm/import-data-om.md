---
title: Import Data and Alerts from Operations Manager
description: Describes how you can import data and alerts from Operations Manager into Service Manager.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 04/11/2025
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.assetid: e233cb46-69de-439d-a4f8-08d8ac993e64
ms.custom: UpdateFrequency3, engagement-fy24
---

# Import data and alerts from Operations Manager into Service Manager


If your organization uses System Center Operations Manager to monitor systems in your enterprise, the agents that are deployed gather information about configuration items that are discovered, and, as problems are detected, System Center Operations Manager generates alerts. Two connectors for Operations Manager are available in Service Manager: the configuration item (CI) connector that imports objects that are discovered by Operations Manager into the Service Manager database, and an alert connector that can create incidents based on alerts.

System Center Operations Manager collects information about many different types of objects, such as hard disk drives and Web sites. To import objects that are discovered by Operations Manager, Service Manager requires a list of class definitions for these objects; the list of definitions is in the System Center Operations Manager management packs. Therefore, you must import some System Center Operations Manager management packs into Service Manager. When you install Service Manager, a set of System Center Operations Manager management packs for common objects and the required Windows PowerShell scripts are copied to your Service Manager installation folder. If you've installed additional management packs in Operations Manager, and you want to add the data from those additional management packs to Service Manager, you can modify the configuration item (CI) connector to add the additional management packs.

The Microsoft Azure management pack for Operations Manager is supported in this release of Service Manager. This means that if an alert from Microsoft Azure is generated in Operations Manager, Service Manager will recognize the alert and an incident can be created.

## Import management packs for Operations Manager configuration item connectors

For the System Center Operations Manager configuration item (CI) connector to function correctly, you've to import a set of management packs into Service Manager. The management packs and the Windows PowerShell script that you need to import the management packs are in the Service Manager installation folder. The default installation folder is \Program Files\Microsoft System Center\Service Manager \<version\>\Operations Manager Management Packs and System Center - Operations Manager Management Packs. Use the following procedures to import the management packs into Service Manager.

To import Operations Manager management packs for an Operations Manager CI connector, follow these steps:

1. On the computer that is hosting the Service Manager management server, on the Windows desktop, select **Start**, point to **Programs**, point to **Windows PowerShell**, right-click **Windows PowerShell**, and select **Run as administrator**.

2. In Windows PowerShell, enter the following command, and then press ENTER:

    ```powershell
    Get-ExecutionPolicy
    ```

3. Review the output and note the current execution policy setting.

4. Enter the following commands, and then press ENTER after each command:

    ```powershell
    Set-ExecutionPolicy Unrestricted
    ```

    ```powershell
    Set-Location \"Program Files\Microsoft System Center \<version\>\Service Manager\Operations Manager Management Packs"
    ```

5. Type the following command, and then press ENTER:

    ```powershell
    .\installOMMPs.ps1
    ```

    This command starts the Windows PowerShell script that installs the management packs. Wait for the management packs to be imported.

6. Change the execution policy back to the value that you noted in step 3. For example, enter the following command to set the execution policy to Restricted, and then press ENTER:

    ```powershell
    Set-ExecutionPolicy Restricted
    ```

7. To exit Windows PowerShell, enter the following command, and then press ENTER:

    ```powershell
    Exit
    ```

### Import Operations Manager management packs for an Operations Manager CI connector

To import Operations Manager management packs for an Operations Manager CI connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Management Packs**.

3. In the **Tasks** pane, under **Management Packs**, select **Import**.

4. In the **Select Management Packs to Import** box, point to the drive where Service Manager is installed, and then point to Program Files\Microsoft System Center\Service Manager \<version\>\Operations Manager \<version\> Management Packs.

5. To the right of the **File name** box, select the file type **MP files (\*.mp)**.

6. In the list of files, select all of the management packs, and select **Open**.

7. In **Import Management Packs**, select all of the management packs, and select **Import**.

8. When the import process is complete, the message *The management pack was imported successfully* will appear.

9. Select **OK**.

## Create an Operations Manager connector

In Service Manager, there are two types of connectors for Operations Manager. You use the first type of connector, the alert connector, to automatically generate incidents that are based on Operations Manager alerts. You use the second type of connector, the configuration item (CI) connector, to import discovered objects from Operations Manager as configuration items into the Service Manager database. You can use the following procedures to create both connectors, validate them, and confirm their creation.

> [!NOTE]
> For the Operations Manager CI connector to function correctly, you've to import a set of management packs into Service Manager.

Alerts that are generated by Operations Manager and that are sent to Service Manager don't contain user information. Therefore, when you open an incident in Service Manager, the **Affected User** box will be empty. You won't be able to save the incident form until you select an affected user. We recommend that you create a special user in Service Manager specifically for this purpose. For more information about how to create a special user, see [How to Manually Create Configuration Items](./config-items.md). This user is the user that you'll assign to the **Affected User** field for all the incidents created by Operations Manager.

You have the option of defining Service Manager templates that run when alerts of certain types are received. If you decide to add an alert routing rule, you can configure Service Manager to use a particular template based on alert criteria such, as priority or severity, as described in the following procedure.

There are two phases for creating the Alert connector. The first part involves creating the Alert connector on the Service Manager management server. The second part requires that you start the Operations Manager console and set up a subscription for the newly created connector. The subscription you create must be unique for the Alert connector; no connector that is created to point to Operations Manager should have a subscription that overlaps with another Operations Manager internal connector. Both phases are described in the following procedure.

### Create an Operations Manager alert connector

To create an Operations Manager alert connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Tasks** pane, under **Connectors**, select **Create Connector**, and select **Operations Manager Alert Connector**.

4. Complete the following steps to complete the Operations Manager Alert Connector Wizard:

   1. On the **Before You Begin** page, select **Next**.

   2. On the **General** page, in the **Name** box, enter a name for the new connector. Ensure that the **Enable** checkbox is selected, and select **Next**. Make a note of this name; you'll need this name in step 7 of this procedure.

   3. On the **Server Details** page, in the **Server name** box, enter the name of the server that is hosting the Operations Manager root management server. Under **Credentials**, select **New**.

   4. In the **Run As Account** dialog, in the **Display name** box, enter a name for this Run As account. In the **Account** list, select **Windows Account**.

   5. In the **User Name**, **Password**, and **Domain** fields, enter the credentials for the Run As account, and select **OK**.

   6. On the **Server Details** page, select **Test Connection**. If you receive the following confirmation message, select **OK**, and select **Next**:

       *The connection to the server was successful.*

   7. On the **Alert Routing Rules** page, select **Add**.

   8. In the **Add Alert Routing Rule** dialog, create a name for the rule, select the template that you want to use to process incidents created by an alert, and then select the alert criteria that you want to use. Select **OK**, and select **Next**.

   9. On the **Schedule** page, select **Close alerts in Operations Manager when incidents are resolved or closed** or **Resolve incidents automatically when the alerts in Operations Manager are closed**, select **Next**, and select **Create**.

5. Start the Operations Manager console.

6. In the **Administration** pane, select **Product Connectors**, and select **Internal Connectors**.

7. In the **Connectors** pane, select the name of the alert connector.

8. In the **Actions** pane, select **Properties**.

9. In the **Alert Sync: *name of connector*** dialog, select **Add**.

10. In the **Product Connector Subscription Wizard** dialog, on the **General** page, in the **Subscription Name** box, enter the name for this subscription. For example, enter **All Alerts**, and select **Next**.

11. On the **Approve groups** page, select **Next**.

12. On the **Approve targets** page, select **Next**.

13. On the **Criteria** page, select **Create**.

14. In the **Alert Sync:*name of connector*** dialog, select **OK**.

### Validate the creation of an Operations Manager alert connector

- Confirm that the connector you created is displayed in the Service Manager console in the **Connectors** pane.

- Confirm that incidents are created in Service Manager from alerts in Operations Manager.

### Create an Operations Manager CI connector

To create an Operations Manager CI connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Tasks** pane, under **Connectors**, select **Create Connector**, and select **Operations Manager CI Connector**.

4. Complete the following steps to complete the Operations Manager CI Connector Wizard:

    1. On the **General** page, in the **Name** box, enter a name for the new connector. Ensure that the **Enable** checkbox is selected, and select **Next**.

    2. On the **Server Details** page, in the **Server name** box, enter the name of the server that is hosting the Operations Manager root management server.

    3. Use one of the following methods to enter credentials:

        - Under **Credentials**, select the Run As account you created for the alert connector, and then go to step 4d.

        - Under **Credentials**, select **New**. In the **User name**, **Password**, and **Domain** boxes, enter the credentials for the Run As account, and select **OK**.

    4. On the **Server Details** page, select **Test Connection**. If you receive the following confirmation message, select **OK**, and select **Next**:

        *The connection to the server was successful.*

    5. On the **MP Selection** page, select **Select all**, or select the management packs that define the configuration items you want to import, and select **Next**.

    6. On the **Schedule** page, select **Next**, and select **Create**.

### Validate the creation of an Operations Manager CI connector

Confirm that the objects that Operations Manager discovered are listed as configuration items in Service Manager.

### Confirm the status of an Operations Manager connector

- View the columns in the **Connector** pane; the columns contain information about the start time, the finish time, the status, and the percentage of import completion.

![PowerShell symbol](./media/import-data-om/pssymbol.png)You can use a Windows PowerShell command to complete these tasks, as follows:

- For information about how to use Windows PowerShell to create a new Operations Manager alert connector in Service Manager, see [New-SCOMAlertConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316238(v=sc.20)).

- For information about how to use Windows PowerShell to create an alert rule to be used with an Operations Manager alert connector in Service Manager, see [New-SCSMAlertRule](/previous-versions/system-center/powershell/system-center-2012-r2/hh316241(v=sc.20)).

- For information about how to use Windows PowerShell to create a new Operations Manager CI connector in Service Manager, see [New-SCOMConfigurationItemConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316228(v=sc.20)).

- For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and to view their status, see [Get-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316209(v=sc.20)).

## Synchronize an Operations Manager connector

When you create an Operations Manager alert connector for Service Manager, it polls Operations Manager every 30 seconds. When you create an Operations Manager configuration item (CI) connector, it synchronizes data from Operations Manager every day at the time you specified in the configured schedule. However, you can use the following procedure to manually synchronize either type of connector.

> [!NOTE]
> The **Start Time** and **Finish Time** values aren't updated when an alert connector is synchronized. These values are only updated when alert data is transferred between Operations Manager and Service Manager.

### Manually synchronize an Operations Manager connector

To manually synchronize an Operations Manager connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Operations Manager connector that you want to synchronize.

4. In the **Tasks** pane, under the connector name, select **Synchronize Now**.

5. In the **Synchronize Now** dialog, select **OK**.

### Validate Operations Manager connector synchronization

To validate Operations Manager connector synchronization, follow these steps:

1. In the Service Manager console, select **Configuration Items**.

2. In the **Configuration Items** pane, expand **Computers**, and select **All Windows Computers**. Verify that any new computers that were discovered in Operations Manager appear in the **All Windows Computers** pane.

## Disable and enable an Operations Manager connector

You can use the following procedures to disable or enable a System Center Operations Manager connector for Service Manager and validate the changes.

For example, after you configure an Operations Manager connector, if you must perform maintenance operations on the Service Manager database, you can temporarily disable the connector and suspend the data import. You can resume the data import by re-enabling the connector.

For more information about how to delete a product connector from System Center Operations Manager, see [Remove an Old Product Connector](/troubleshoot/system-center/scom/remove-old-product-connectors) on Kevin Holman's System Center blog.

### Disable an Operations Manager connector

To disable an Operations Manager connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Operations Manager connector that you want to disable.

4. In the **Tasks** pane, under the connector name, select **Disable**.

5. In the **Disable Connector** dialog, select **OK**.

### Enable an Operations Manager connector

To enable an Operations Manager connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Operations Manager connector that you want to enable.

4. In the **Tasks** pane, under the connector name, select **Enable**.

5. In the **Enable Connector** dialog, select **OK**.

### Validate the status change of an Operations Manager connector

To validate the status change of an Operations Manager connector, follow these steps:

1. Wait 30 seconds. Then, in the Service Manager console, select **Administration**, and select **Connectors**.

2. In the **Connectors** pane, locate the connector for which you've changed the status, and verify the value in the **Enabled** column.

![PowerShell symbol](./media/import-data-om/pssymbol.png)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

- For information about how to use Windows PowerShell to start a Service Manager connector, see [Start-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316244(v=sc.20)).

- For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and view their status, see [Get-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316209(v=sc.20)).

- For information about how to use Windows PowerShell to update the properties of a Service Manager connector, see [Update-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316217(v=sc.20)).

## Edit an Operations Manager connector

After you install an Operations Manager alert connector and configuration item (CI) connector, you can edit the connectors. For example, you can use the following procedure to add more management packs to the CI connector.

To edit an Operations Manager CI connector, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Operations Manager connector that you want to edit.

4. In the **Tasks** pane, under the connector name, select **Properties**.

5. In the **Edit** dialog, in the left pane, select **Management Packs**.

6. In the **Management Packs** pane, select **Refresh**.

7. In the **Credentials** dialog, enter the credentials to connect to Operations Manager, and select **OK**.

8. In the **Management Packs** list, select the management packs that define the configuration items that you want to import, and select **OK**.

## Next steps

Learn about how to [Import data from Configuration Manager](import-data-cm.md).
