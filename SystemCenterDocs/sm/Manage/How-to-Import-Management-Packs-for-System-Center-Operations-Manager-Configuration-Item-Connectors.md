---
title: How to Import Management Packs for System Center Operations Manager Configuration Item Connectors
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a2f96b5b-22fe-4e1a-b832-1ed2a22e2d13
---
# How to Import Management Packs for System Center Operations Manager Configuration Item Connectors
For the System Center Operations Manager configuration item \(CI\) connector to function correctly, you have to import a set of management packs into Service Manager. The management packs and the Windows PowerShell script that you need to import the management packs are in the [!INCLUDE[smshort](../../includes/smshort_md.md)] installation folder. The default installation folder is \\Program Files\\Microsoft System Center\\Service Manager 2016\\Operations Manager Management Packs and System Center 2016 \- Operations Manager Management Packs. Use the following procedures to import the management packs into [!INCLUDE[smshort](../../includes/smshort_md.md)].

### To import Operations Manager management packs for an Operations Manager CI connector

1.  On the computer that is hosting the [!INCLUDE[smshort](../../includes/smshort_md.md)] management server, on the Windows desktop, click **Start**, point to **Programs**, point to **Windows PowerShell**, right click **Windows PowerShell**, and then click **Run as administrator**.

2.  In Windows PowerShell, type the following command, and then press ENTER:

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

### To import System Center \- Operations Manager management packs for an Operations Manager CI connector

1.  On the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Tasks** pane, under **Management Packs**, click **Import**.

4.  In the **Select Management Packs to Import** box, point to the drive where [!INCLUDE[smshort](../../includes/smshort_md.md)] is installed, and then point to Program Files\\Microsoft System Center\\Service Manager 2016\\Operations Manager 2016 Management Packs.

5.  To the right of the **File name** box, select the file type **MP files \(\*.mp\)**.

6.  In the list of files, select all of the management packs, and then click **Open**.

7.  In **Import Management Packs**, select all of the management packs, and then click **Import**.

8.  When the import process is complete, the message “The management pack was imported successfully” will appear.

9. Click **OK**.


