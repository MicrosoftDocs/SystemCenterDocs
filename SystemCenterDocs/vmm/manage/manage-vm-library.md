---
ms.assetid: e756446f-f0bb-428f-a054-a33087fad435
title: Deploy a virtual machine from the VMM library
description: This article describes how to create VMs in the VMM fabric from the VMM library
author:  rayne-wiselman
ms-author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Deploy a virtual machine from the VMM library

>Applies To: System Center 2016 - Virtual Machine Manager


This article describes how to deploy a virtual machine that's stored in the System Center 2016 - Virtual Machine Manager (VMM) library.

## Before you start

- You need one or more VMs stored in the VMM library. To store a VM in the library the VM must be stopped, shutdown, or saved. You can't store a VM while it's running.
- To store a VM in the library select the VM > **Actions** > **Store in Library**. In the Select Library Server Wizard, specify where you want to store the VM. Then click **Store** to move the VM to the library. Review progress on the **Jobs** tab.

## Deploy a VM

1. In **Library** workspace, navigate to the library server on which the VM is stored, and then click **Stored Virtual Machines and Services**.
2. Select the VM on the **Virtual Machines** tab > **Actions**, click **Deploy**.
3. In Deploy Virtual Machine Wizard > **Select Host**, select a host on which to deploy the VM. All available hosts are given a rating of 0–5 stars, based on their suitability to host the virtual machine. You can select any host that has the required disk space, even if the host has a zero host rating. [Learn more](../provision-vms.md#vm-placement).

    - In **Network optimization**, if a host has network optimization enabled, a green check mark appears.
    - In **Highly available virtual machines**, to make a VM highly available, you can migrate it to a host in a cluster, even if the VM hasn't been configured as highly available. Conversely, you can migrate a highly available VM to a standalone host.
    -   **Details**: Indicates the status of the host, the operating system, and the type and status of the virtualization software.
    -   **Rating Explanation**: Provides an explanation if a host received a zero rating.
    -   **SAN Explanation** or **Deployment and Transfer Explanation**: Lists any factors that make a storage area network (SAN) transfer unavailable. VMM does not recognize a virtual machine that is stored on a SAN as available for deployment by using SAN transfer if the virtual machine was stored directly in the library when it was created or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same VMM library, library share, and logical unit number (LUN).
    - The **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers (ODX). [Learn more](http://technet.microsoft.com/library/hh831628.aspx).
4. In **Select Path**, specify where you want to store the configuration files for the VM.

    - If you didn't select the default path, and you want to store other VMs on the path, select **Add this path to the list of host default paths**.
    - If SAN transfers are enabled for this deployment, by default, the virtual machine is transferred to the host over the storage area network (SAN). If you do not want to perform a SAN transfer, select the Transfer over the network even if a SAN transfer is available check box. If SAN transfers are not available for this deployment, this option is not available.
5. In **Select Networks**, select the network settings the VM should use.
6. In **Summary**, review the settings, and then click **Deploy**. You can select to start the VM after it's deployed.

## Next steps

[Manage the VM settings](../vm-settings.md)
