---
ms.assetid: 224a6e43-cce0-4d27-92ba-1c551e9366c0
title: Deploy and manage Update Rollups in System Center Data Protection Manager
description: This article provides information about how to deploy and manage the update rollups in System Center DPM.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: article
ms.service: system-center
ms.subservice: data-protection-manager
ms.custom: intro-deployment, UpdateFrequency2, engagement-fy24
---

# Deploy and manage update rollups in Data Protection Manager

This article provides information about how to install and verify update rollups (UR) for System Center - Data Protection Manager (DPM).

>[!NOTE]
> Update Rollups are installed automatically if Microsoft Updates are set to *Automatic*. If these are not installed automatically, you can install manually.

## Obtain and install update rollups

The following sections provide information about how to obtain and install the Update Rollups manually through Microsoft updates, Microsoft Download Center, and DPM command line.

### Back up the DPM database

Back up the DPM database as detailed [here](back-up-the-dpm-server.md#back-up-with-native-sql-server-backup-to-a-local-disk).

>[!NOTE]
> Verify that the job completes successfully. If the job fails, review the error details and redo the backup.

### Install update rollups from Microsoft updates

Follow these steps on a computer that has DPM installed, and latest updates are yet to be installed:

1. Under **Settings** > **Update & Security**, select **Windows Update**.
1. In the **Windows Update** window, select **Check Online for updates from Microsoft Update**.
1. Select **Important updates are available**.
1. Select the update rollup package and then select **OK**.
1. Select **Install updates** to install the update package.

### Install update rollups from Microsoft Download Center

To manually download the update rollups from the Microsoft download center, [visit](https://www.catalog.update.microsoft.com/Home.aspx) the Microsoft Download Center, search for the desired KB, and manually download the update rollup packages.

### Install update rollups manually through command prompt

To manually install an update rollup package through an elevated command prompt, do the following steps:

1. Run the following command to extract the package, select the path for extraction when prompted. 
 
    ```console
    <DPMUR exe name> /x
    ```

1. From the extracted location, run the following command to install the update rollup:

    ```console
    msiexec.exe/update <package_name>

    ```

    For example, to install the Update Rollup 2 (KB4563392) for DPM 2019, run the following command:

    ```console
    msiexec.exe/update kb4563392_DPMserver_amd64.msp
    ```

    >[!NOTE]
    > There may be additional installation steps specific to a UR. Check the relevant KB article to ensure you complete all the installation steps.

### Check the installation of an update rollup

Use the following procedure to check if an update rollup is successfully installed:

1. Under **Control Panel** > **Programs and Features** > **View installed updates**.

2. Verify that an update entry was created after the update rollup was installed.

   For example, the 2019 update rollup 2 was released as 4563392. You should be able to see this detail under **View installed updates** if you've installed this update rollup and if it was successfully installed.

3. Verify that the binary's version has the correct build number. 

4. See the [list of build numbers for DPM](release-build-versions.md) to check the build number for a specific update rollup.

> [!NOTE]
> Not all the binaries have the current update rollup build number. However, if you do not have the binaries listed with the relevant update rollup build number, it is likely that the update rollup did not install successfully.

## Next steps

See [what's new in the latest update rollup](what-s-new-in-dpm.md)
