---
ms.assetid: 829e4ab1-2f23-4113-b294-b8f7c387a28a
title: Clone VMs from another VM in the VMM fabric
description: This article describes how to clone VMs in the VMM fabric from another VM
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Clone VMs from another VM in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to create and deploy virtual machines by cloning existing VMs in the System Center 2016 - Virtual Machine Manager (VMM) fabric.


## Before you start

- To complete the steps you must be an Administrator or Delegated Administrator on the VMM server, or a self-service user.
- When you clone a virtual machine, the existing virtual machine source is not deleted. We recommend that you clone a virtual machine that has been prepared and generalized with the Sysprep tool. If you do not use a generalized virtual hard disk, the identity of the new virtual machine will be the same as the source. Issues might occur if you turn on two virtual machines with the same identity at the same time.
- You can clone a virtual machine that is deployed on a host. The machine can be online, stopped, or in a saved state.
- You can clone a VM that is stored in the VMM library.
- The option to use differencing disk optimizations is automatically applied when you deploy the virtual machine on a host, if a base disk exists on that host.
- If you're a self-service user you need **Deploy** permissions with the **Store and re-deploy** action assigned. You must first deploy the VM to a private cloud, and then store it in the library.

## Create a VM

1.  Click **VMs and Services** > **Create Virtual Machine** > **Create Virtual Machine**.
2. In **Create Virtual Machine Wizard** > **Select Source**, click **Use an existing virtual machine, VM template, or virtual hard disk** > **Browse**. Select an existing VM.
3. In **Select Source**, click **Next**.
4. In **Configure Hardware**, optionally configure any available settings. Then click **Next**.
5.  In **Select Destination** page, specify how the virtual machine should be deployed - in a private cloud, on a host, or stored in the library.



## Deploy the VM in a private cloud

1.  In **Select Cloud** select the private cloud on which you want to place the virtual machine. If you are connected as an Administrator, you can select the host on which the virtual machine should be deployed in the private cloud. Cloud suggestions are based on a 0-5 star rating. [Learn more](manage-vm-overview.md#vm-placement). Verify the settings and modify if required:

    -   **Expected utilization**: Expected utilization for a VM created from a blank VHD is based on standard defaults. VMM updates host suggestions and ratings in response to modifications made to the expected virtual machine utilization.
    -   **Make this VM highly available**: With this option selected, only hosts that are located in a cluster are available for selection.
    -   **Details**: Indicates the status of the host, the operating system, and the type and status of the virtualization software.
    -   **Rating Explanation**: Provides an explanation if a host received a zero rating.
    -   **SAN Explanation** or **Deployment and Transfer Explanation**: Lists any factors that make a storage area network (SAN) transfer unavailable. VMM does not recognize a virtual machine that is stored on a SAN as available for deployment by using SAN transfer if the virtual machine was stored directly in the library when it was created or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same VMM library, library share, and logical unit number (LUN).
    - The **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers (ODX). [Learn more](http://technet.microsoft.com/library/hh831628.aspx).

2.  In **Configure Settings**, review the VM settings. Either accept the default VM path on the host or specify a different location. you can optionally select to **Add this path to the list of default virtual machine paths on the host**. In **Machine Resources** accept the default values for the VHD, or modify as required. To prevent placement from choosing its own values, click the pin icon next to the setting. This option isn't available for self-service users.
3.  In **Select Networks**, if it appears, optionally select the network settings, and click **Next**.
4.  In **Add Properties**, configure the action to take when the host starts or stops, and the operating system that you will install on the VM. Then click **Next.**
5.  In **Summary**, confirm the settings, and click **Create**. Confirm that the VM was created in **VMs and Services** > **Clouds**, and select the cloud. The virtual machine appears in the **VMs** pane.

## Deploy the VM on a host

1. In **Select Host**, view the ratings, click the host on which you want to deploy the VM, and click **Next**. The host suggestions are based on a 0-5 star rating. [Learn more](manage-vm-overview.md#vm-placement). Verify the settings and modify if required:

    -   **Expected utilization**: Expected utilization for a VM created from a blank VHD is based on standard defaults. VMM updates host suggestions and ratings in response to modifications made to the expected virtual machine utilization.
    -   **Make this VM highly available**: With this option selected, only hosts that are located in a cluster are available for selection.
    -   **Details**: Indicates the status of the host, the operating system, and the type and status of the virtualization software.
    -   **Rating Explanation**: Provides an explanation if a host received a zero rating.
    -   **SAN Explanation** or **Deployment and Transfer Explanation**: Lists any factors that make a storage area network (SAN) transfer unavailable. VMM does not recognize a virtual machine that is stored on a SAN as available for deployment by using SAN transfer if the virtual machine was stored directly in the library when it was created or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same VMM library, library share, and logical unit number (LUN).
    - The **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers (ODX). [Learn more](http://technet.microsoft.com/library/hh831628.aspx).
2.  In **Configure Settings**, review the VM settings. Either accept the default VM path on the host or specify a different location. you can optionally select to **Add this path to the list of default virtual machine paths on the host**. In **Machine Resources** accept the default values for the VHD, or modify as required. To prevent placement from choosing its own values, click the pin icon next to the setting. This option isn't available for self-service users.
3. In **Select Networks**, if it appears, optionally select the network settings, and click **Next**.
4. In **Add Properties**, configure the action to take when the host starts or stops, and the operating system that you will install on the VM. Then click **Next.**
5.  On the **Summary** page, confirm the settings, and then click **Create**.


## Store the VM in the library

1.  In **Select Library Server**, click the library server that you want to use, and then click **Next**.
2.  In **Select Path**, specify the library share location to store the virtual machine. Click **Browse** to select a library share and an optional folder location, click **OK**, and then click **Next**.
3.  In **Summary** confirm the settings, and then click **Create**.
4.  To confirm that the virtual machine was created, in the **Library** workspace, in the **Library** pane, expand **Library Servers**, expand the library server where you stored the virtual machine, and then click **Stored Virtual Machines and Services**. The stored virtual machine appears in the **Physical Library Objects** pane.

## Next steps

- [Manage the VM settings](manage-vm-settings.md)
