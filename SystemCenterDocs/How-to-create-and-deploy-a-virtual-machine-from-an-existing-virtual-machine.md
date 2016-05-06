---
title: How to create and deploy a virtual machine from an existing virtual machine
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b6ebb7-3278-46e8-9dc4-535d456c6169
---
# How to create and deploy a virtual machine from an existing virtual machine
Use the following procedure to use [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] to create a virtual machine by *cloning* an existing virtual machine. You can also use cloning to create backups of existing virtual machines.

Note the following:

-   You must be a member of the Administrator or Delegated Administrator user role, or a self\-service user who has the **Deploy** action in the scope of the role to complete this procedure.

-   When you clone a virtual machine, the existing virtual machine source is not deleted. We recommend that you clone a virtual machine that has been prepared and generalized with the Sysprep tool. If you do not use a generalized virtual hard disk, the identity of the new virtual machine will be the same as the source. Issues might occur if you turn on two virtual machines with the same identity at the same time.

-   You can clone a virtual machine that is deployed on a host, or a virtual machine that is stored in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library. Starting with hosts running [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)], virtual machines can be cloned when they're online, stopped, or in a saved state. Otherwise, virtual machines must be stopped or in a saved state.

-   The option to use differencing disk optimizations is automatically applied when you deploy the virtual machine on a host, if a base disk exists on that host.

-   For a self\-service user to store a virtual machine in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library, the following is required:

    1.  The self\-service user role must have the **Store and re\-deploy** action assigned.

    2.  The self\-service user must first deploy the virtual machine to a private cloud, and then store it in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library.

## Creating a virtual machine
Use the following procedure to create a virtual machine from an existing virtual machine.

#### To create a virtual machine from an existing virtual machine

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Create** group, click the **Create Virtual Machine** drop\-down arrow, and then click **Create Virtual Machine**.

    The **Create Virtual Machine Wizard** opens.

3.  On the **Select Source** page, ensure that **Use an existing virtual machine, VM template, or virtual hard disk** is selected, click **Browse**, click the existing virtual machine, and then click **OK**.

4.  On the **Select Source** page, click **Next**.

5.  On the **Identity**\/**Specify Virtual Machine Identity** page, enter a new name for the virtual machine name and an optional description.

6.  On the **Configure Hardware** page, optionally configure any available settings, and then click **Next**.

7.  On the **Select Destination** page, select one of the following:

    -   Select **Deploy the virtual machine to a private cloud** to place the virtual machine in an existing private cloud. Then follow the instructions in [Deploying the virtual machine in a private cloud](#BKMK_Cloud).

    -   Select **Place the virtual machine on a host** to place the virtual machine on an existing virtual machine host. Then follow the instructions in [Deploying the virtual machine on a host](#BKMK_Host).

    -   Select **Store the virtual machine in the library** to store the virtual machine before deployment. Then follow the instructions in [Storing the virtual machine in the library](#BKMK_Library).

### <a name="BKMK_Cloud"></a>Deploying the virtual machine in a private cloud

1.  On the **Select Cloud** page, select the private cloud on which you want to place the virtual machine. If you are connected as an administrator, you can select the host on which the virtual machine should be deployed in the private cloud. The cloud suggestions are based on a 0\-5 star rating. For more information, see [Understanding virtual machine placement and ratings in VMM](./Understanding-virtual-machine-placement-and-ratings-in-VMM.md). Verify the settings and modify them if required:

    -   **Expected utilization**—For a virtual machine that is created from a blank hard disk, the expected utilization is based on standard defaults. For a virtual machine created that is created from an existing virtual machine, the default settings are based on past performance of the existing virtual machine. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] updates host suggestions and ratings in response to modifications that are made to the expected virtual machine utilization.

    -   **Make this VM highly available**—With this option selected, only hosts that are located in a cluster are available for selection.

    -   **Details**—Indicates the status of the host, the operating system, and the type and status of virtualization software.

    -   **Rating Explanation**—Provides an explanation if a host received a zero rating.

    -   **SAN Explanation** or **Deployment and Transfer Explanation**—Lists any factors that make a storage area network \(SAN\) transfer unavailable. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] does not recognize a virtual machine that is stored on a SAN as available for deployment using SAN transfer if the virtual machine was stored directly in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library when it was created, or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library, library share, and logical unit number \(LUN\).

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers \(ODX\) feature, introduced in [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)]. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

2.  On the **Configure Settings** page, review the virtual machine settings:

    1.  In **Locations**, either accept the default virtual machine path on the host for storing the virtual machine files, or click **Browse** to specify a different location. Optionally, select the **Add this path to the list of default virtual machine paths on the host** check box.

    2.  In **Machine Resources**, click **Virtual Hard Disk**. Accept the default values or select a different destination path on the host for the virtual hard drive file \(.vhd or .vhdx file\). To change the file name, enter a new name in the **File name** box.

    > [!TIP]
    > To prevent placement from choosing a different value for these settings, click the pin icon next to the setting. Note that self\-service users do not see this option.

3.  On the **Select Networks** page, if the page appears, optionally select the logical network that you want to use, the virtual network, and the virtual LAN \(VLAN\) ID, if applicable, and then click **Next**.

4.  On the **Add Properties** page, configure the action to take when the host starts or stops, and then click **Next**.

5.  On the **Summary** page, confirm the settings, and then click **Create**. To confirm that the virtual machine was created, in the **VMs and Services** workspace, in the **VMs and Services** pane, expand **Clouds**, and then click the private cloud where you deployed the virtual machine. On the **Home** tab, in the **Show** group, click **VMs**. The virtual machine appears in the **VMs** pane.

### <a name="BKMK_Host"></a>Deploying the virtual machine on a host

1.  On the **Select Host** page, review the placement ratings and transfer type, click a host, and then click **Next**. Note the following settings:

    -   **Expected Utilization**—For a virtual machine that is created from a blank hard disk, the expected utilization is based on standard defaults. For a virtual machine that is created from an existing virtual machine, the default settings are based on past performance of the existing virtual machine. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] updates host suggestions and ratings in response to modifications that are made to the expected virtual machine utilization.

    -   **Make this VM highly available**—With this option selected, only hosts in a cluster available for selection.

    -   **Details**—Indicates the status of the host, the operating system, and the type and status of virtualization software.

    -   **Rating Explanation**—Provides an explanation if a host received a zero rating.

    -   **SAN Explanation** or **Deployment and Transfer Explanation**—Lists any factors that make a storage area network \(SAN\) transfer unavailable. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] does not recognize a virtual machine that is stored on a SAN as available for deployment using SAN transfer if the virtual machine was stored directly in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library when it was created, or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library, library share, and logical unit number \(LUN\).

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers \(ODX\) feature, introduced in [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)]. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

2.  On the **Configure Settings** page, review the settings for the virtual machine:

    1.  In **Locations**, either accept the default virtual machine path on the host for storing the virtual machine files, or click **Browse** to specify a different location. Optionally, select the **Add this path to the list of default virtual machine paths on the host** check box.

    2.  In **Machine Resources**, click **Virtual Hard Disk**. Accept the default values, or select a different destination path on the host for the virtual hard drive file \(.vhd or .vhdx file\). To change the file name, enter a new name in the **File name** box.

    > [!TIP]
    > To prevent placement from choosing a different value for these settings, click the pin icon next to the setting. Note that self\-service users do not see this option.

3.  On the **Select Networks** page, accept or change the logical network, virtual network, or VLAN ID if applicable, and then click **Next**.

4.  On the **Add Properties** page, configure the action to take when the host starts or stops. Then click **Next**.

5.  On the **Summary** page, confirm the settings, and then click **Create**.

### <a name="BKMK_Library"></a>Storing the virtual machine in the library

1.  On the **Select Library Server** page, click the library server that you want to use, and then click **Next**.

2.  On the **Select Path** page, specify the library share location to store the virtual machine. Click **Browse** to select a library share and optional folder location, click **OK**, and then click **Next**.

3.  On the **Summary** page, confirm the settings, and then click **Create**.

    To confirm that the virtual machine was created, in the **Library** workspace, in the **Library** pane, expand **Library Servers**, expand the library server where you stored the virtual machine, and then click **Stored Virtual Machines and Services**. The stored virtual machine appears in the **Physical Library Objects** pane.

## See Also
[Creating and deploying virtual machines in VMM](./Creating-and-deploying-virtual-machines-in-VMM.md)
[Configuring virtual machine options and settings](./Configuring-virtual-machine-options-and-settings.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)
[Managing virtual machines with VMM](./Managing-virtual-machines-with-VMM.md)


