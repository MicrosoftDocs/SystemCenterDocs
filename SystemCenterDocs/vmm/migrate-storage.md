---
ms.assetid: 57fb5b26-923e-4d33-8195-aeab83db9443
title: Migrate storage in the VMM fabric
description: This article describes how to migrate storage in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/20/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Migrate storage in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to migrate storage in the VMM fabric

Storage migration enables you to move VM files from one storage location to another, on the same VM host. If the virtual machine is running, you can perform a quick storage migration, which results in little or no service outage for users of the virtual machine. If the virtual machine has more than one virtual hard disk, you can specify a separate location for each virtual hard disk (.vhd or .vhdx) file.

[Read this article](migrate-live.md#migrate-storage-between-two-locations-on-a-standalone-host) if you want to run a live migration of VM storage between two locations on a standalone host.

Run the migration as follows:

1.  In **VM"s and Services**, click **All Hosts**, and then select the host on which the virtual machine is deployed.

2.  Right-click the virtual machine > **Migrate Storage**.

    The Migrate Storage Wizard opens at the **Select Path** page. The current location of the VM configuration files is displayed in the **Storage location for VM configuration**, and the current location of each virtual hard disk (.vhd) is displayed in **Disks**.

3.  On the **Select Path** page, do the following:

    - In **Storage location for VM configuration** select an existing default virtual machine path on the list. Browse to a location on the host. VMM automatically changes the paths for all virtual disks to the same path that you specified for the configuration files.
    - Type a path. When you type a new path for the configuration files of the virtual machine, VMM does not automatically change the paths for the virtual disks until you click outside of the **Storage location for VM configuration** box.
    - Select the **Add this path to the list of default storage locations on the host** check box, if you selected a path other than an existing virtual machine path, and you want to add the path to the default paths on the host.
    - Specify the configuration file placement options, as follows:

        1.  Select **Automatically place all VHDs with the configuration** to move all of the virtual machine files to the same location.
        2.  Select **Allow VHDs to be placed individually** to move one or more of the virtual machine files to a different location than the location of the configuration files. If you select this setting, in the **Disks** area, type the new path in the **Location** box for each virtual hard disk, or click **Browse** to browse to the location where you want to store the file. Note that if the virtual machine is running, and you change the path for any of the virtual hard drives, you also must specify a new path for the configuration files of the virtual machine, or the migration operation fails. You must enter the new path even if you want to leave the configuration files in their current location. In that case, you can create a new subfolder within the current location of the configuration files, and then select that new location in the **Storage location for VM configuration** box.

4.  On the **Summary** page, click **Move** to begin moving the virtual machine files. Review progress in **Jobs**.
