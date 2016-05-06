---
title: Tasks to Perform Before Beginning the VMM Upgrade
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4452d461-4240-4d4f-b619-0f6bf362ce2f
---
# Tasks to Perform Before Beginning the VMM Upgrade
Before you can install [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)], you need to uninstall the current version of [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] and prepare the environment by performing the following tasks:

1.  Review [Planning Considerations for Upgrading VMM](./Planning-Considerations-for-Upgrading-VMM.md).

2.  Complete all jobs that are currently running in VMM. You can use the console to view the jobs’ status. All job history is deleted during the upgrade.

3.  Close any connections to the VMM management server, including the VMM console and the VMM command shell.

4.  Close any other programs that are running on the VMM management server.

5.  Ensure that there are no pending restarts on the computers on which the VMM roles are installed. For example, if you have installed a server role by using Server Manager or have applied a security update, you may need to restart the computer. After you have restarted the computer, sign in to the computer with the same user account to finish the installation of the server role or the security update.

6.  If Windows Azure Hyper\-V Recovery Manager is implemented in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] environment, ensure that version 3.3.140.0 or later of Windows Azure Hyper\-V Recovery Manager Provider is installed on the VMM management server. After the upgrade, you will need to re\-install the Windows Azure Hyper\-V Recovery Manager Provider, to ensure that it works properly.

7.  Perform a full backup of the VMM database. For more information, see [Back up and restore VMM](./Back-up-and-restore-VMM.md). You can also use tools that are provided by SQL Server to back up the VMM database. For more information, see [Back Up and Restore of SQL Server Databases](http://technet.microsoft.com/library/ms187048.aspx).

8.  Uninstall the following:

    -   All components of [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)]. On the **Uninstallation Options** page, click **Retain data**. For more information on how to uninstall the current VMM console, see [How to Uninstall VMM](./How-to-Uninstall-VMM.md).

    -   Windows Automated Installation Kit \(Windows AIK\).

9. Ensure that the server meets all requirements for [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)] as described in System Requirements for System Center vNext and in [Preparing your environment for System Center 2016 - Virtual Machine Manager](./Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

    -   If needed, upgrade SQL Server to a supported version, as described in SQL Server Requirements for System Center vNext. If the current version is supported in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)], this upgrade is not required.

    -   Install[Windows 8.1 Assessment and Deployment Kit (Windows ADK)](http://www.microsoft.com/download/details.aspx?id=39982).

10. If the current database is configured with AlwaysOn Availability Groups, complete the following tasks:

    -   If the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database is included in the availability group, remove it. You can use the Microsoft SQL Management Studio tool to perform this task.

    -   Initiate a failover to the computer that is running SQL Server and on which the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database is installed.

11. You can now upgrade [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

## See Also
[Performing a VMM Upgrade](./Performing-a-VMM-Upgrade.md)


