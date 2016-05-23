---
title: How to create and deploy a virtual machine from a blank virtual hard disk
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d0d6fac-dab5-4e97-9751-1f4035b6aa01
---
# How to create and deploy a virtual machine from a blank virtual hard disk
Use the following procedure to create a virtual machine from a blank virtual hard disk in [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)]. After you create the virtual machine, you can install an operating system from an .iso image, from a CD or DVD, or from a network boot if a Pre\-Boot Execution Environment \(PXE\) server is available.

Before you complete this procedure, note the following:

-   To complete the procedure, you must be a member of the Administrator or Delegated Administrator user role, or you must be a self\-service user who has the **Deploy** action in the scope of their user role.

-   For a self\-service user to store a virtual machine in the library, the following is required:

    -   The self\-service user role must have the **Store and re\-deploy** action assigned.

    -   The self\-service user must first deploy the virtual machine to a private cloud, and then store it in the library.

-   You can customize static IP address settings only if you create a virtual machine from a virtual machine template.

-   You can use [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to configure the availability settings for the virtual machine. For more information, see [Configuring availability options for virtual machines in VMM](Configuring-availability-options-for-virtual-machines-in-VMM.md).

## Creating a virtual machine
Use the following procedure to create a virtual machine from a blank virtual hard disk.

#### To create a virtual machine from a blank virtual hard disk

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, click the **Create Virtual Machine** drop\-down arrow, and then click **Create Virtual Machine**.

    The **Create Virtual Machine Wizard** opens.

3.  On the **Select Source** page, click **Create the new virtual machine with a blank virtual hard disk**, and then click **Next**.

4.  On the **Identity** page, enter the virtual machine name and an optional description. In the **Generation** box, select **Generation 1** or **Generation 2**. For more information, see [Understanding generation 1 and generation 2 virtual machines in VMM](Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md). Then click **Next**.

5.  On the **Configure Hardware** page, either select the profile that you want to use from the **Hardware profile** list, or configure the hardware settings manually, and then click **Next**. Note the following:

    -   In **Compatibility**, if you want to deploy the virtual machine to a private cloud, select a capability profile that is available to the private cloud.

    -   The hardware profiles and hardware options that are available are those of the generation that you selected in the previous step. For more information, see [Understanding generation 1 and generation 2 virtual machines in VMM](Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md).

    -   In **Bus Configuration**, if you want to install an operating system from a DVD or an .iso image, ensure there is a virtual DVD drive that is configured to use an available option such as the **Existing ISO image file** option. If you want to use an ISO image file, the file must be present in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library.

    -   If you want to store the virtual machine in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library before you deploy it to a host, use of one of the blank virtual hard disks that by default are provided in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library. Do this as follows:

        1.  In **Bus Configuration**, click the virtual hard disk.

        2.  In the details pane, click **Use an existing virtual hard disk**. Then click **Browse**. Click one of the blank disk choices, and then click **OK**.

    -   If the virtual machine is a generation 1 virtual machine that will boot from the network to install an operating system, in **Network Adapters**, use the legacy network adapter type. This type is indicated by the network adapter name, for example, **Legacy Network Adapter 1**.

6.  On the **Select Destination** page, specify how the virtual machine should be deployed:

    -   Select **Deploy the virtual machine to a private cloud** to place the virtual machine in an existing private cloud. Then follow the instructions in[Deploying the virtual machine in a private cloud](#BKMK_Cloud).

    -   Select **Place the virtual machine on a host** to place the virtual machine on an existing virtual machine host. Then follow the instructions in [Deploying the virtual  machine on a host](#BKMK_Host).

    -   Select **Store the virtual machine in the library** to store the virtual machine. Then follow the instructions in [Storing the virtual machine in the library](#BKMK_Library).

### <a name="BKMK_Cloud"></a>Deploying the virtual machine in a private cloud
Use the following procedure to deploy the virtual machine in a private cloud.

##### To deploy the virtual machine in a private cloud

1.  On the **Select Cloud** page, select the private cloud on which you want to place the virtual machine. If you are connected as an Administrator, you can select the host on which the virtual machine should be deployed in the private cloud. The cloud suggestions are based on a 0\-5 star rating. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md). Verify the settings and modify if required:

    -   **Expected utilization**—For a virtual machine that is created from a blank hard disk, the expected utilization is based on standard defaults. For a virtual machine that is created from an existing virtual machine, the default settings are based on past performance of the existing machine. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] updates host suggestions and ratings in response to modifications made to the expected virtual machine utilization.

    -   **Make this VM highly available**—With this option selected, only hosts that are located in a cluster are available for selection.

    -   **Details**—Indicates the status of the host, the operating system, and the type and status of the virtualization software.

    -   **Rating Explanation**—Provides an explanation if a host received a zero rating.

    -   **SAN Explanation** or **Deployment and Transfer Explanation**—Lists any factors that make a storage area network \(SAN\) transfer unavailable. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not recognize a virtual machine that is stored on a SAN as available for deployment by using SAN transfer if the virtual machine was stored directly in the library when it was created or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library, library share, and logical unit number \(LUN\).

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers \(ODX\) feature, introduced in [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)]. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

2.  On the **Configure Settings** page, review the virtual machine settings:

    1.  In **Locations**, either accept the default virtual machine path on the host to store the virtual machine files, or click **Browse** to specify a different location. Optionally, select the **Add this path to the list of default virtual machine paths on the host** check box.

    2.  In **Machine Resources**, click **Virtual Hard Disk**. Accept the default values, or select a different destination path on the host for the virtual hard drive file \(.vhd or .vhdx file\). To change the file name, enter a new name in the **File name** box.

    > [!TIP]
    > To prevent placement from choosing a different value for these settings, click the pin icon next to the setting. Note that self\-service users do not see this option.

3.  On the **Select Networks** page, if the page appears, optionally, select the virtual machine network that you want to use, the virtual network, and the virtual LAN \(VLAN\) ID, if applicable, and then click **Next**.

4.  On the **Add Properties** page, configure the action to take when the host starts or stops, and the operating system that you will install on the virtual machine. Click **Next.**

5.  On the **Summary** page, confirm the settings, and then click **Create**. To confirm that the virtual machine was created, in the **VMs and Services** workspace, in the **VMs and Services** pane, expand **Clouds**, and then click the private cloud where you deployed the virtual machine. On the **Home** tab, in the **Show** group, click **VMs**. The virtual machine appears in the **VMs** pane.

### <a name="BKMK_Host"></a>Deploying the virtual machine on a host
Use the following procedure to deploy the virtual machine on a host.

##### To deploy the virtual machine on a host

1.  On the **Select Host** page, view the ratings, click the host on which you want to deploy the virtual machine, and then click **Next**. The host suggestions are based on a 0\-5 star rating. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md). Note the following settings:

    -   **Expected utilization**—For a virtual machine that is created from a blank hard disk, the expected utilization is based on standard defaults. For a virtual machine that is created from an existing virtual machine, the default settings are based on past performance of the existing machine. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] updates host suggestions and ratings in response to modifications that are made to the expected virtual machine utilization.

    -   **Make this VM highly available**—With this option selected, only hosts that are in a cluster are available for selection.

    -   **Details**—Indicates the status of the host, the operating system, and the type and status of the virtualization software.

    -   **Rating Explanation**—Provides an explanation if a host received a zero rating.

    -   **SAN Explanation** or **Deployment and Transfer Explanation**—Lists any factors that make a SAN transfer unavailable. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] does not recognize a virtual machine that is stored on a SAN as available for deployment by using SAN transfer if the virtual machine was stored directly in the library when it was created or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library, library share, and logical unit number \(LUN\).

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers \(ODX\) feature, introduced in [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)]. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

2.  On the **Configure Settings** page, review the settings for the virtual machine:

    1.  In **Locations**, either accept the default virtual machine path on the host to store the virtual machine files, or click **Browse** to specify a different location. Optionally, select the **Add this path to the list of default virtual machine paths on the host** check box.

    2.  In **Machine Resources**, click **Virtual Hard Disk**. Accept the default values, or select a different destination path on the host for the virtual hard drive file \(.vhd or .vhdx file\). To change the file name, enter a new name in the **File name** box.

    > [!TIP]
    > To prevent placement from choosing a different value for these settings, click the pin icon next to the setting. Note that self\-service users do not see this option.

3.  On the **Select Networks** page, if the page appears, optionally, select the virtual machine network that you want to use, the virtual network, and the virtual LAN \(VLAN\) ID, if applicable, and then click **Next**.

4.  On the **Add Properties** page, configure the action to take when the host starts or stops, and the operating system to install on the virtual machine. Then click **Next**.

5.  On the **Summary** page, confirm the settings, and then click **Create**.

### <a name="BKMK_Library"></a>Storing the virtual machine in the library
Use the following procedure to store the virtual machine in the library.

##### To store the virtual machine in the library

1.  On the **Select Library Server** page, click the library server that you want to use, and then click **Next**.

2.  On the **Select Path** page, specify the library share location to store the virtual machine. Click **Browse** to select a library share and an optional folder location, click **OK**, and then click **Next**.

3.  On the **Summary** page, confirm the settings, and then click **Create**.

4.  To confirm that the virtual machine was created, in the **Library** workspace, in the **Library** pane, expand **Library Servers**, expand the library server where you stored the virtual machine, and then click **Stored Virtual Machines and Services**. The stored virtual machine appears in the **Physical Library Objects** pane.

## See Also
[Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md)
[Configuring virtual machine options and settings](Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


