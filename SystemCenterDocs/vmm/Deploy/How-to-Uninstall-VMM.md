---
title: How to Uninstall VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34ead8d2-f244-4d8a-95f2-e985b7c69976
---
# How to Uninstall VMM
You can use the following procedures to uninstall a VMM management server or the VMM console.

Before uninstalling VMM, ensure that the VMM console and the VMM command shell are closed.

> [!NOTE]
> If there is a problem with uninstallation completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

Membership in the local Administrators group, or equivalent, on the computer that you are configuring is the minimum required to complete these procedures.

### To uninstall a VMM management server

1.  On the computer on which the VMM management server is installed, click **Start**, and then click **Control Panel**.

2.  Under **Programs**, click **Uninstall a program**.

3.  Under **Name**, double-click **Microsoft System Center 2016 Virtual Machine Manager**.

4.  On the **What would you like to do?** page, click **Remove features**.

5.  On the **Select features to remove** page, select the **VMM management server** check box, and then click **Next**.

    > [!NOTE]
    > If you also want to uninstall the VMM console, select the **VMM console** check box.

6.  On the **Database options** page, select whether you want to retain or remove the VMM database, and, if necessary, credentials for the database, and then click **Next**.

7.  On the **Summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Uninstall** to uninstall the VMM management server.

    After you click **Uninstall**, the **Uninstalling features** page appears and uninstallation progress is displayed.

8.  After the VMM management server is uninstalled, on the **The selected features were removed successfully** page, click **Close**.

The following firewall rules, which were enabled during VMM Setup, remain in effect after you uninstall VMM:

-   File Server Remote Management

-   Windows Standards-Based Storage Management firewall rules

> [!NOTE]
> If there is a problem with setup completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

### To uninstall the VMM console

1.  On the computer on which the VMM console is installed, click **Start**, and then click **Control Panel**.

2.  Under **Programs**, click **Uninstall a program**.

3.  Under **Name**, double-click **Microsoft System Center 2016 Virtual Machine Manager**.

4.  On the **What would you like to do?** page, click **Remove features**.

5.  On the **Select features to remove** page, select the **VMM console** check box, and then click **Next**.

    > [!NOTE]
    > If a VMM management server is also installed on the computer, you must also uninstall the VMM management server.

6.  On the **Summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Uninstall** to uninstall the VMM console.

    After you click **Uninstall**, the **Uninstalling features** page appears and uninstallation progress is displayed.

7.  After the VMM console is uninstalled, on the **The selected features were removed successfully** page, click **Close**.


