---
ms.assetid: e756446f-f0bb-428f-a054-a33087fad435
title: Deploy VMs from the VMM library
description: This article describes how to create VMs in the VMM fabric from the VMM library
author: jyothisuri
ms.author: jsuri
ms.date: 08/30/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-deployment, UpdateFrequency3, engagement-fy24
---


# Deploy a virtual machine from the VMM library



This article describes how to deploy a virtual machine that's stored in the System Center Virtual Machine Manager (VMM) library.

## Before you start

- You need one or more VMs stored in the VMM library. To store a VM in the library, the VM must be stopped, shut down, or saved. You can't store a VM while it's running.
- To store a VM in the library, select the VM > **Actions** > **Store in Library**. In the Select Library Server Wizard, specify where you want to store the VM. Select **Store** to move the VM to the library. Review progress on the **Jobs** tab.

## Deploy a VM

1. In the **Library** workspace, navigate to the library server on which the VM is stored, and then select **Stored Virtual Machines and Services**.
2. Select the VM on the **Virtual Machines** tab > **Actions**, select **Deploy**.
3. In Deploy Virtual Machine Wizard > **Select Host**, select a host on which to deploy the VM. All available hosts are given a rating of 0–5 stars based on their suitability to host the virtual machine. You can select any host that has the required disk space, even if the host has a zero host rating. To learn more, review [VM placement](provision-vms.md#vm-placement).

    - In **Network optimization**, if a host has network optimization enabled, a green check mark appears.
    - In **Highly available virtual machines**, to make a VM highly available, you can migrate it to a host in a cluster, even if the VM hasn't been configured as highly available. Conversely, you can migrate a highly available VM to a standalone host.
    -   **Details**: Indicates the status of the host, the operating system, and the type and status of the virtualization software.
    -   **Rating Explanation**: Provides an explanation if a host received a zero rating.
    -   **SAN Explanation** or **Deployment and Transfer Explanation**: Lists any factors that make a storage area network (SAN) transfer unavailable. VMM doesn't recognize a virtual machine that is stored on a SAN as available for deployment using SAN transfer if the virtual machine was stored directly in the library when it was created or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host using a LAN transfer, and then store the virtual machine in the same VMM library, library share, and logical unit number (LUN).
    - The **Deployment and Transfer Explanation** tab provides an explanation if fast file copy can't be used. Fast file copy is based on the Windows Offloaded Data Transfers (ODX). To learn more, review [overview of Windows ODX](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831628(v=ws.11)).
4. In **Select Path**, specify where you want to store the configuration files for the VM.

    - If you didn't select the default path, and you want to store other VMs on the path, select **Add this path to the list of host default paths**.
    - If SAN transfers are enabled for this deployment, by default, the virtual machine is transferred to the host over the storage area network (SAN). If you don't want to perform a SAN transfer, select the **Transfer over the network even if a SAN transfer is available** checkbox. If SAN transfers aren't available for this deployment, this option isn't available.
5. In **Select Networks**, select the network settings the VM must use.
6. In **Summary**, review the settings, and select **Deploy**. You can select to start the VM after it's deployed.

## Next steps

[Manage the VM settings](vm-settings.md)
