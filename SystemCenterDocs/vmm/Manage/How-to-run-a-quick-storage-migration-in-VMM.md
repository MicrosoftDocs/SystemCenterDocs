---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to run a quick storage migration in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  a0bdcd69-546e-435a-a2b6-8a85a8c5fb64
---

# How to run a quick storage migration in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Use the following procedure to run a *quick storage migration* in Virtual Machine Manager (VMM). Quick storage migration enables you to move the files of a virtual machine from one storage location to another on the same virtual machine host. If the virtual machine is running, you can perform a quick storage migration, which results in little or no service outage for users of the virtual machine. If the virtual machine has more than one virtual hard disk, you can specify a separate location for each virtual hard disk (.vhd or .vhdx) file.

Use the following procedure to run a quick storage migration.

### To run a quick storage migration

1.  In the VMM console, open the **VM"s and Services** workspace. In the **VM"s and Services** pane, expand **All Hosts**, and then select the host on which the virtual machine is deployed.

2.  In the **VM"s** pane, right-click the virtual machine, and then click **Migrate Storage**.

    The Migrate Storage Wizard opens at the **Select Path** page. It displays the current locations of the virtual machine"s files. The current path to the location of the configuration files is displayed in the **Storage location for VM configuration** box, and the current path to the location of each virtual hard disk (.vhd) is displayed in the **Disks** list.

3.  On the **Select Path** page, do the following:

    -   Configure a storage location for the virtual machine configuration, by doing one of the following:

        -   Click the **Browse** button next to **Storage location for VM configuration**, and then click an existing default virtual machine path on the list.

        -   Click the **Browse** button next to **Storage location for VM configuration** and browse to a location on the host. VMM automatically changes the paths for all virtual disks to the same path that you specified for the configuration files.

        -   Type a path. When you type a new path for the configuration files of the virtual machine, VMM does not automatically change the paths for the virtual disks until you click outside of the **Storage location for VM configuration** box.

    -   Select the **Add this path to the list of default storage locations on the host** check box, if you selected a path other than an existing virtual machine path, and you want to add the path to the default paths on the host.

    -   Specify the configuration file placement options, as follows:

        1.  Select **Automatically place all VHDs with the configuration** to move all of the virtual machine files to the same location.

        2.  Select **Allow VHDs to be placed individually** to move one or more of the virtual machine files to a different location than the location of the configuration files. If you select this setting, in the **Disks** area, type the new path in the **Location** box for each virtual hard disk, or click **Browse** to browse to the location where you want to store the file. Note that if the virtual machine is running, and you change the path for any of the virtual hard drives, you also must specify a new path for the configuration files of the virtual machine, or the migration operation fails. You must enter the new path even if you want to leave the configuration files in their current location. In that case, you can create a new subfolder within the current location of the configuration files, and then select that new location in the **Storage location for VM configuration** box.

4.  On the **Summary** page, click **Move** to begin moving the virtual machine files.

5.  To review the progress and results of the operation, open the **Jobs** pane. By default, this pane opens after the wizard closes. To view this pane at any time, click **Jobs** on the VMM console toolbar.




