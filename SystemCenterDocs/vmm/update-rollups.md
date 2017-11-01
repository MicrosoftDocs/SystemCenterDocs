---
ms.assetid: 58a686bd-2b59-4c73-ab41-6e3c8fc200c0
title: Deploy and manager update rollups in VMM 2016
description: This article provides information about how to deploy and manage the update rollups in System Center 2016 - VMM.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: riyazp
ms.date: 11/01/2017
ms.topic: article
ms.prod:  system-center-threshold
ms.technology: virtual-machine-manager
---

# Deploy and manage update rollups in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

This article provides information about how to install, verify, and remove update rollups for System Center Virtual Machine Manager (VMM).

>[!NOTE]
> Update rollups are installed automatically if Microsoft Updates are set to Automatic. If they are not installed automatically, you can install these manually.
>

## Obtain and install update rollups

The following sections provide information about how to obtain and install the update rollups manually through Microsoft updates, Microsoft Download Center and through VMM command line.

### Back up the VMM database

1. In the VMM console, click **Settings**.
1. On the Home tab, click **Backup**.
1. In the VMM backup page, in the **Path** text box, specify the location for the backup file, and then click **OK**.

>[!NOTE]
> Verify that the job completes successfully, otherwise review the error details, and redo the backup.
>

More information: [Back up the VMM database](backup.md#back-up-the-vmm-database) 

### Install update rollups from Microsoft updates

Follow these steps on a computer that has a VMM component installed and latest updates are yet to be installed:

1. Under **Settings** > **Update & Security**, click **Windows Update**.
1. In the **Windows Update** window, click **Check Online for updates from Microsoft Update**.
1. Click **Important updates are available**.
1. Select the update rollup package and then click **OK**.
1. Click **Install updates** to install the update package.

### Install update rollups from Microsoft Download Center

To manually download the update rollups from the Microsoft download center, [visit](http://www.catalog.update.microsoft.com/Home.aspx) the Microsoft Download Center, search for the desired KB and manually download the update rollup packages.

### Install update rollups through command prompt

To manually install an update rollup package through an elevated command prompt, run the following command:

**msiexec.exe/update <package_name>**

>[!NOTE]
> In the **<package_name>** placeholder, enter the actual package name.
>

For example, to install the Update Rollup 2 for System Center 2016 Virtual Machine Manager server (KB3209586), run the following command:

**msiexec.exe/update kb3209586_VMMserver_amd64.msp**

>[!NOTE]
> There may be additional installation steps specific to an update rollup release. Check update rollup KB guide to ensure you complete all the installation steps.
>

### Check the installation of an update rollup

Use the following procedure to check if an update rollup is successfully installed:

1. Under **Control Panel** > **Programs and Features** > **View installed updates**.
1. Verify that an update entry was created after the update rollup was installed.
    - For example, the Update Rollup 2 was released as update 3209586. You should be able to see this detail under **View installed updates** if you have installed this update rollup and if it was successfully installed.
1. Verify that the binary's version has the correct build number. 
1. See the following website to check the build number for a specific update rollup:
    - [List of build numbers for VMM](https://social.technet.microsoft.com/wiki/contents/articles/15361.system-center-virtual-machine-manager-list-of-build-numbers.aspx)

> [!NOTE]
> Not all the binaries have the current update rollup build number. However, if you do not have the binaries listed with the relevant update rollup build number, it is likely that the update rollup did not install successfully.
>

## Remove an update rollup

> [!IMPORTANT]
> 1. It is not recommended that you remove the update rollups. Prior to removing, check all the available options if you can avoid the uninstall. You may also contact Microsoft Support to check and ensure if uninstallation is required.
> 1. It is recommended that you [back up your VMM database](backup.md#back-up-the-vmm-database) before you attempt to remove an update rollup.
> 1. When you remove, the VMM binaries roll back to their earlier versions. However, the VMM database does not roll back.
> 1. If you have one or more hotfixes installed on the server, make sure that you replace the hotfix binary with the official update rollup binary, before you start the removal.
>

### Remove an update rollup by using the control panel

1. Go to **Control Panel** > **Programs** > **Programs and Features**. For quick access, type **appwiz.cpl** in **Run** it opens the **Programs and Features** in **Control Panel**.
1. Click **View installed updates**.
1. Find the update that you want to remove, right-click the update, and then select **Uninstall**.

### Remove an update rollup by using the command line
> [!NOTE]
> To remove an update by using the command line, you must have the following two globally unique identifiers (GUIDs) available:
>
>- RTM product GUID
>- Patch GUID
>

#### RTM Product GUIDs

- SCVMM Server: {EBC28D9B-9565-46F3-A248-E26F07F81A98}
- SCVMM Admin Console amd64: {B703D43A-ABF6-4A36-84CC-00D77FF8570B}
- SCVMM Admin Console i386: {F5D46892-E1BD-4E0A-BD6E-DAA1900BA786}
- SCVMM Guest Agent amd64: {3E71E1FB-AF93-4110-A8EB-973132A3B16B}
- SCVMM Guest Agent i386: {57D2C983-23BF-4840-B784-BDDAC2DC932B}

#### Patch GUIDs

To find the patch GUID, right-click the update, select **Properties**. On the **Details** tab, and then select **Revision number**. This is the patch GUID.

When you know the RTM product GUID and the patch GUID, run the following command to remove the update:
 
**Msiexec /I {< RTM Product GUID >} MSIPATCHREMOVE={< Patch GUID >}**

### Verify the successful removal of an update rollup

Use the following procedure to check if the update rollup was successfully removed:

1. Check whether the update was removed from **Programs and Features**. 
1. Verify that binaries were reverted successfully. To do this, go to the VMM installation directory, and verify that there is no binary that has the build version of the update rollup that you uninstalled. 

> [!NOTE]
> When you uninstall the server and console updates from the VMM server, the order of uninstallation is not important.
>

### Restore the database backup in VMM

> [!NOTE]
> 1. You can create a database backup at any time. But the database should be restored only if you uninstalled the latest update rollup on the server. If you uninstalled an older update rollup, you do not have to restore the VMM database.
> 1. Ensure that you restore the database backup that you created prior to the update rollup installation.
>

For information on how to restore the database back up, see [this article](backup.md#restore-the-vmm-environment).

### Post-restore tasks

This section applies only if you add a host or a library server after you create a database backup and before you uninstall an update rollup.

After the VMM database is recovered, you must do the following actions:

- Remove any hosts that were removed from VMM since the last backup.
- If a host was removed since the last backup, the host shows a status of **Needs Attention** in the VMM console. Also, the virtual machines on that host show a status of **Host Not Responding**.
- Remove the virtual machines that were removed from the VMM since the last back up. If a host has a virtual machine that was removed since the last backup, the virtual machine shows a status of **Missing** in the VMM console.
- Add any hosts that were added to the VMM since the last backup.
- If you restored the VMM database to a different computer, you must re-associate the hosts that have a status of **Access Denied** in the VMM console.
  - A computer is considered different if it has a different security identifier (SID). For example, if you reinstall the operating system on the computer, the computer has a different SID, even if it has the same computer name.

For more information on post-restore tasks,  see [this article](backup.md#post-restore-tasks).

> [!NOTE]
> You must follow these steps for any other fabric resource such as storage providers, library servers, and so on that you add after you create a database backup.
>
