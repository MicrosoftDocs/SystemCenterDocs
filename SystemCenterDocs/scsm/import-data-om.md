---
title: Import data and alerts from Operations Manager
description: Describes how you can import data and alerts from Operations Manager into Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: e233cb46-69de-439d-a4f8-08d8ac993e64
---

# Import data and alerts from Operations Manager into Service Manager

>Applies To: System Center 2016 - Service Manager

If your organization uses System Center Operations Manager to monitor systems in your enterprise, the agents that are deployed gather information about configuration items that are discovered, and, as problems are detected, System Center Operations Manager generates alerts. Two connectors for Operations Manager are available in Service Manager: the configuration item (CI) connector that imports objects that are discovered by Operations Manager into the Service Manager database, and an alert connector that can create incidents based on alerts.

System Center Operations Manager collects information about many different types of objects, such as hard disk drives and Web sites. To import objects that are discovered by Operations Manager, Service Manager requires a list of class definitions for these objects; the list of definitions is in the System Center Operations Manager management packs. Therefore, you must import some System Center Operations Manager management packs into Service Manager. When you install Service Manager, a set of System Center Operations Manager management packs for common objects and the required Windows PowerShell scripts are copied to your Service Manager installation folder. If you have installed additional management packs in Operations Manager, and you want to add the data from those additional management packs to Service Manager, you can modify the configuration item (CI) connector to add the additional management packs.

The Microsoft Azure management pack for Operations Manager is supported in this release of Service Manager. This means that if an alert from Microsoft Azure is generated in Operations Manager, Service Manager will recognize the alert and an incident can be created.

## Import management packs for Operations Manager configuration item connectors

For the System Center Operations Manager configuration item (CI) connector to function correctly, you have to import a set of management packs into Service Manager. The management packs and the Windows PowerShell script that you need to import the management packs are in the Service Manager installation folder. The default installation folder is \Program Files\Microsoft System Center\Service Manager 2016\Operations Manager Management Packs and System Center 2016 - Operations Manager Management Packs. Use the following procedures to import the management packs into Service Manager.

### To import Operations Manager management packs for an Operations Manager CI connector

1.  On the computer that is hosting the Service Manager management server, on the Windows desktop, click **Start**, point to **Programs**, point to **Windows PowerShell**, right click **Windows PowerShell**, and then click **Run as administrator**.

2.  In Windows PowerShell, type the following command, and then press ENTER:

    ```
    Get-ExecutionPolicy
    ```

3.  Review the output and note the current execution policy setting.

4.  Type the following commands, and then press ENTER after each command:

    ```
    Set-ExecutionPolicy Unrestricted
    ```

    ```
    Set-Location \"Program Files\Microsoft System Center 2016\Service Manager\Operations Manager Management Packs"
    ```

5.  Type the following command, and then press ENTER:

    ```
    .\installOMMPs.ps1
    ```

    This command starts the Windows PowerShell script that installs the management packs. Wait for the management packs to be imported.

6.  Change the execution policy back to the value that you noted in step 3. For example, type the following command to set the execution policy to Restricted, and then press ENTER:

    ```
    Set-ExecutionPolicy Restricted
    ```

7.  To exit Windows PowerShell, type the following command, and then press ENTER:

    ```
    Exit
    ```

### To import Operations Manager management packs for an Operations Manager CI connector

1.  On the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Tasks** pane, under **Management Packs**, click **Import**.

4.  In the **Select Management Packs to Import** box, point to the drive where Service Manager is installed, and then point to Program Files\Microsoft System Center\Service Manager 2016\Operations Manager 2016 Management Packs.

5.  To the right of the **File name** box, select the file type **MP files (\*.mp)**.

6.  In the list of files, select all of the management packs, and then click **Open**.

7.  In **Import Management Packs**, select all of the management packs, and then click **Import**.

8.  When the import process is complete, the message *The management pack was imported successfully* will appear.

9. Click **OK**.

## Create an Operations Manager connector

In Service Manager, there are two types of connectors for Operations Manager. You use the first type of connector, the alert connector, to automatically generate incidents that are based on Operations Manager alerts. You use the second type of connector, the configuration item (CI) connector, to import discovered objects from Operations Manager as configuration items into the Service Manager database. You can use the following procedures to create both connectors, validate them, and confirm their creation.

> [!NOTE]
> For the Operations Manager CI connector to function correctly, you have to import a set of management packs into Service Manager.

Alerts that are generated by Operations Manager and that are sent to Service Manager do not contain user information. Therefore, when you open an incident in Service Manager, the **Affected User** box will be empty. You will not be able to save the incident form until you select an affected user. We recommend that you create a special user in Service Manager specifically for this purpose. For more information about how to create a special user, see [How to Manually Create Configuration Items](admin-how-to-manually-create-configuration-items.md). This user is the user that you will assign to the **Affected User** field for all incidents created by Operations Manager.

You have the option of defining Service Manager templates that run when alerts of certain types are received. If you decide to add an alert routing rule, you can configure Service Manager to use a particular template based on alert criteria such, as priority or severity, as described in the following procedure.

There are two phases for creating the Alert connector. The first part involves creating the Alert connector on the Service Manager management server. The second part requires that you start the Operations Manager console and set up a subscription for the newly created connector. The subscription you create must be unique for the Alert connector; no connector that is created to point to Operations Manager should have a subscription that overlaps with another Operations Manager internal connector. Both phases are described in the following procedure.

### To create an Operations Manager alert connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Operations Manager Alert Connector**.

4.  Complete the following steps to complete the Operations Manager Alert Connector Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that the **Enable** check box is selected, and then click **Next**. Make a note of this name; you will need this name in step 7 of this procedure.

    3.  On the **Server Details** page, in the **Server name** box, type the name of the server that is hosting the Operations Manager root management server. Under **Credentials**, click **New**.

    4.  In the **Run As Account** dialog box, in the **Display name** box, type a name for this Run As account. In the **Account** list, select **Windows Account**.

    5.  In the **User Name**, **Password**, and **Domain** fields, type the credentials for the Run As account, and then click **OK**.

    6.  On the **Server Details** page, click **Test Connection**. If you receive the following confirmation message, click **OK**, and then click **Next**:

        *The connection to the server was successful.*

    7.  On the **Alert Routing Rules** page, click **Add**.

    8.  In the **Add Alert Routing Rule** dialog box, create a name for the rule, select the template that you want to use to process incidents created by an alert, and then select the alert criteria that you want to use. Click **OK**, and then click **Next**.

    9. On the **Schedule** page, select **Close alerts in Operations Manager when incidents are resolved or closed** or **Resolve incidents automatically when the alerts in Operations Manager are closed**, click **Next**, and then click **Create**.

5.  Start the Operations Manager console.

6.  In the **Administration** pane, click **Product Connectors**, and then click **Internal Connectors**.

7.  In the **Connectors** pane, click the name of the alert connector.

8.  In the **Actions** pane, click **Properties**.

9. In the **Alert Sync: *name of connector*** dialog box, click **Add**.

10. In the **Product Connector Subscription Wizard** dialog box, on the **General** page, in the **Subscription Name** box, type the name for this subscription. For example, type **All Alerts**, and then click **Next**.

11. On the **Approve groups** page, click **Next**.

12. On the **Approve targets** page, click **Next**.

13. On the **Criteria** page, click **Create**.

14. In the **Alert Sync:*name of connector*** dialog box, click **OK**.

### To validate the creation of an Operations Manager alert connector

-   Confirm that the connector you created is displayed in the Service Manager console in the **Connectors** pane.

-   Confirm that incidents are created in Service Manager from alerts in Operations Manager.

### To create an Operations Manager CI connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Operations Manager CI Connector**.

4.  Complete the following steps to complete the Operations Manager CI Connector Wizard:

    1.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that the **Enable** check box is selected, and then click **Next**.

    2.  On the **Server Details** page, in the **Server name** box, type the name of the server that is hosting the Operations Manager root management server.

    3.  Use one of the following methods to enter credentials:

        -   Under **Credentials**, select the Run As account you created for the alert connector, and then go to step 4d.

        -   Under **Credentials**, click **New**. In the **User name**, **Password**, and **Domain** boxes, type the credentials for the Run As account, and then click **OK**.

    4.  On the **Server Details** page, click **Test Connection**. If you receive the following confirmation message, click **OK**, and then click **Next**:

        *The connection to the server was successful.*

    5.  On the **MP Selection** page, click **Select all**, or select the management packs that define the configuration items you want to import, and then click **Next**.

    6.  On the **Schedule** page, click **Next**, and then click **Create**.

### To validate the creation of an Operations Manager CI connector

-   Confirm that the objects that Operations Manager discovered are listed as configuration items in Service Manager.

### To confirm the status of an Operations Manager connector

-   View the columns in the **Connector** pane; the columns contain information about the start time, the finish time, the status, and the percentage of import completion.

![PowerShell symbol](./media/import-data-om/pssymbol.png)You can use a Windows PowerShell command to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to create a new Operations Manager alert connector in Service Manager, see [New-SCOMAlertConnector](https://go.microsoft.com/fwlink/p/?LinkID=225351).

-   For information about how to use Windows PowerShell to create an alert rule to be used with an Operations Manager alert connector in Service Manager, see [New-SCSMAlertRule](https://go.microsoft.com/fwlink/p/?LinkId=225353).

-   For information about how to use Windows PowerShell to create a new Operations Manager CI connector in Service Manager, see [New-SCOMConfigurationItemConnector](https://go.microsoft.com/fwlink/p/?LinkID=225352).

-   For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and to view their status, see [Get-SCSMConnector](https://go.microsoft.com/fwlink/p/?LinkId=225320).

## Synchronize an Operations Manager connector

When you create an Operations Manager alert connector for Service Manager, it polls Operations Manager every 30 seconds. When you create an Operations Manager configuration item (CI) connector, it synchronizes data from Operations Manager every day at the time you specified in the configured schedule. However, you can use the following procedure to manually synchronize either type of connector.

> [!NOTE]
> The **Start Time** and **Finish Time** values are not updated when an alert connector is synchronized. These values are only updated when alert data is transferred between Operations Manager and Service Manager.

### To manually synchronize an Operations Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to synchronize.

4.  In the **Tasks** pane, under the connector name, click **Synchronize Now**.

5.  In the **Synchronize Now** dialog box, click **OK**.

### To validate Operations Manager connector synchronization

1.  In the Service Manager console, click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Computers**, and then click **All Windows Computers**. Verify that any new computers that were discovered in Operations Manager appear in the **All Windows Computers** pane.

## Disable and enable an Operations Manager connector

You can use the following procedures to disable or enable a System Center Operations Manager connector for Service Manager and validate the changes.

For example, after you configure an Operations Manager connector, if you must perform maintenance operations on the Service Manager database, you can temporarily disable the connector and suspend the data import. You can resume the data import by re-enabling the connector.

For more information about how to delete a product connector from System Center Operations Manager, see [Removing an Old Product Connector](https://go.microsoft.com/fwlink/?LinkId=188974) on Kevin Holman's System Center blog.

### To disable an Operations Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to disable.

4.  In the **Tasks** pane, under the connector name, click **Disable**.

5.  In the **Disable Connector** dialog box, click **OK**.

### To enable an Operations Manager connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to enable.

4.  In the **Tasks** pane, under the connector name, click **Enable**.

5.  In the **Enable Connector** dialog box, click **OK**.

### To validate the status change of an Operations Manager connector

1.  Wait 30 seconds. Then, in the Service Manager console, click **Administration**, and then click **Connectors**.

2.  In the **Connectors** pane, locate the connector for which you have changed the status, and verify the value in the **Enabled** column.

![PowerShell symbol](./media/import-data-om/pssymbol.png)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to start a Service Manager connector, see [Start-SCSMConnector](https://go.microsoft.com/fwlink/p/?LinkId=225378).

-   For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and view their status, see [Get-SCSMConnector](https://go.microsoft.com/fwlink/p/?LinkId=225320).

-   For information about how to use Windows PowerShell to update the properties of a Service Manager connector, see [Update-SCSMConnector](https://go.microsoft.com/fwlink/p/?LinkID=225382).

## Edit an Operations Manager connector

After you install an Operations Manager alert connector and configuration item (CI) connector, you can edit the connectors. For example, you can use the following procedure to add more management packs to the CI connector.

### To edit an Operations Manager CI connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Operations Manager connector that you want to edit.

4.  In the **Tasks** pane, under the connector name, click **Properties**.

5.  In the **Edit** dialog box, in the left pane, click **Management Packs**.

6.  In the **Management Packs** pane, click **Refresh**.

7.  In the **Credentials** dialog box, enter the credentials to connect to Operations Manager, and then click **OK**.

8.  In the **Management Packs** list, select the management packs that define the configuration items that you want to import, and then click **OK**.

## Next steps

- Learn about how to [Import data from Configuration Manager](import-data-cm.md).
