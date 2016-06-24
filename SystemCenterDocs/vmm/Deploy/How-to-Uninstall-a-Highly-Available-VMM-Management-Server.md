---
title: How to Uninstall a Highly Available VMM Management Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d664710d-7e8e-4f83-a4b2-2979197aa099
---
# How to Uninstall a Highly Available VMM Management Server
You can use the following procedures to uninstall a highly available Virtual Machine Manager (VMM) management server. To uninstall high availability completely, you will need to uninstall highly available VMM management server from each node in the cluster.

Before uninstalling VMM, ensure that the VMM console and the VMM command shell are closed. If you are uninstalling an additional node of a highly available VMM management server, use Failover Cluster Manager to ensure that the node is not currently the owner of the highly available service. If the node is the current owner, move the service to another node in the cluster.

Membership in the local Administrators group, or equivalent, on the computer that you are configuring is the minimum required to complete these procedures.

### To uninstall an additional node of a highly available VMM management server

1.  On a computer on which the highly available VMM management server is installed, click **Start**, and then click **Control Panel**.

2.  Under **Programs**, click **Uninstall a program**.

3.  Under **Name**, double-click **Microsoft System Center 2012 Virtual Machine Manager**.

4.  On the **What would you like to do?** page, click **Remove features**.

5.  On the **Select features to remove** page, select the **VMM management server** check box, and then click **Next**.

    > [!NOTE]
    > If you also want to uninstall the VMM console, select the **VMM console** check box.

6.  On the **Database options** page, click **Next**.

7.  On the **Summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Uninstall** to uninstall the VMM management server.

    After you click **Uninstall**, the **Uninstalling features** page appears and uninstallation progress is displayed.

8.  After the VMM management server is uninstalled, on the **The selected features were removed successfully** page, click **Close**.

### To uninstall the last node of a highly available VMM management server

1.  On the last node on which the highly available VMM management server is installed, click **Start**, and then click **Control Panel**.

2.  Under **Programs**, click **Uninstall a program**.

3.  Under **Name**, double-click **Microsoft System Center 2012 Virtual Machine Manager**.

4.  On the **What would you like to do?** page, click **Remove features**.

5.  On the **Select features to remove** page, select the **VMM management server** check box.

6.  When you are prompted whether you want to uninstall the last node of the highly available VMM management server, click **Yes**.

7.  On the **Select features to remove** page, click **Next**.

    > [!NOTE]
    > If you also want to uninstall the VMM console, select the **VMM console** check box.

8.  On the **Database options** page, select whether you want to retain or remove the VMM database, and, if necessary, enter credentials for the database, and then click **Next**.

    > [!IMPORTANT]
    > If you select **Retain database**, you can only use this database with a highly available VMM management server installation. The retained database cannot be used with a standalone installation of VMM management server.

9. On the **Summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Uninstall** to uninstall the VMM management server.

10. After you click **Uninstall**, the **Uninstalling features** page appears and uninstallation progress is displayed.

11. After the VMM management server is uninstalled, on the **The selected features were removed successfully** page, click **Close**.

> [!NOTE]
> If there is a problem with uninstallation completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.


