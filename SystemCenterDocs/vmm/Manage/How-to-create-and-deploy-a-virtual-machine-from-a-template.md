---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to create and deploy a virtual machine from a template
ms.technology:  virtual-machine-manager
ms.assetid:  2b37e839-f245-4e51-83ec-e2c11864a10b
---

# How to create and deploy a virtual machine from a template

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Use the following procedure to create a virtual machine from a virtual machine template in Virtual Machine Manager (VMM). You can use a virtual machine template to create new stand-alone virtual machines or to create tiers in a service template. 

Note the following:

-   Server roles and features, application installation, and settings on an instance of Microsoft SQL Server apply only when a virtual machine template is used for service deployments. For stand-alone virtual machine creation, these settings are not used and are not visible when you use a template with these settings to create a virtual machine.

-   To configure a virtual machine to use static IP addresses from an IP address pool that is managed by VMM, you must use a virtual machine template as the source.

-   To complete this procedure, you must be a member of the Administrator, the Delegated Administrator, or the self-service user role.

-   For a self-service user to deploy a virtual machine from a template, the following is required:

    -   The self-service user role must have the **Deploy** or **Deploy (From template only)** actions in their user role scope.

    -   The template must be available to the self-service user role as an assigned resource, or the self-service user role must be granted access in the template properties.

-   You can use VMM to configure availability settings for the virtual machine. 

## Creating a virtual machine
Use the following procedure to create a virtual machine from a template.

#### To create a virtual machine from a template

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Create** group, click the **Create Virtual Machine** drop-down arrow, and then click **Create Virtual Machine**.

    The Create Virtual Machine Wizard opens.

3.  On the **Select Source** page, ensure that **Use an existing virtual machine, VM template, or virtual hard disk** is selected, and then click **Browse**.

4.  In the **Select Virtual Machine Source** dialog box, click the appropriate virtual machine template, and then click **OK**.

    > [!NOTE]
    > If the template contains Windows Server roles and features, application deployment, or SQL Server deployment settings, you receive a message that these settings will be ignored for stand-alone virtual machine deployment. Click **OK** to continue.

5.  On the **Select Source** page, click **Next**.

6.  On the **Identity**/**Specify Virtual Machine Identity** page, enter the virtual machine name and optional description, and then click **Next**.

7.  On the **Configure Hardware** page, either select the profile that you want to use from the **Hardware profile** list, or configure the hardware settings manually. After you have configured the hardware settings, click **Next**. Note the following:

    -   In **Capability**, you must select a capability profile that is supported by the private cloud.

    -   In **Network Adapters**, if you configure a network adapter to use static IP addresses, you must also set the MAC address to **Static**.

    -   In**Network Adapters**, for a virtual machine that uses a virtual hard disk in the VMware .vmdk format, be sure to include a legacy network adapter in the template. To add a legacy network adapter, at the top, in the **New** bar, click **Network Adapter**, and then, in the drop-down box, click **Legacy network adapter**. If you do not include a legacy network adapter when you use the .vmdk format, when you deploy the virtual machine, the virtual machine might not be able to start in a domain, although it can start in a workgroup.

    -   On the **Configure Operating System** page, configure the guest operating system settings. If you have an existing guest operating system profile that you want to use, in the **Guest OS profile** list, click the guest operating system profile that you want to use. After you configure the guest operating system settings, click **Next**.

8.  On the **Select Destination** page, specify how to deploy the virtual machine:

    -   Select **Deploy the virtual machine to a private cloud** to place the virtual machine in an existing private cloud. Then follow the instructions in [Deploying the virtual machine in a private cloud](#BKMK_Cloud).

    -   Select **Place the virtual machine on a host** to place the virtual machine on an existing virtual machine host. Then follow the instructions in [Deploying the virtual machine on a host](#BKMK_Host).

    -   Select **Store the virtual machine in the library** to store the virtual machine. Then follow the instructions in [Storing the virtual machine in the library](#BKMK_Library).

### <a name="BKMK_Cloud"></a>Deploying the virtual machine in a private cloud

1.  On the **Select Cloud** page, select the private cloud on which you want to place the virtual machine.  If you are connected as an administrator, you can select the host on which the virtual machine should be deployed in the private cloud. The cloud suggestions are based on a 0-5 star rating. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md). Verify the settings and modify them if required:

    -   **Expected utilization**�For a virtual machine that is created from a blank hard disk, the expected utilization is based on standard defaults. For a virtual machine that is created from an existing virtual machine, the default settings are based on past performance of the existing virtual machine. VMM updates host suggestions and ratings in response to modifications that are made to the expected virtual machine utilization.

    -   **Make this VM highly available**�With this option selected, only hosts that are located in a cluster are available for selection.

    -   **Details**�Indicates the status of the host, the operating system, and the type and status of virtualization software.

    -   **Rating Explanation**�Provides an explanation if a host received a zero rating.

    -   **SAN Explanation** or **Deployment and Transfer Explanation**�Lists any factors that make a storage area network (SAN) transfer unavailable. VMM does not recognize a virtual machine that is stored on a SAN as available for deployment using SAN transfer if the virtual machine was stored directly in the VMM library when it was created, or was added to the library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same VMM library, library share, and logical unit number (LUN).

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers (ODX) feature, introduced in Windows Server 2012 R2. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

2.  On the **Configure Settings** page, confirm or change the computer name, and then click **Next**.

3.  On the **Add Properties** page, configure the action to take when the host starts or stops. If you are a VMM administrator, to prevent the virtual machine from being migrated by Performance and Resource Optimization (PRO) or dynamic optimization, select the **Exclude virtual machine from optimization actions** check box. Then click **Next**.

4.  On the **Summary** page, confirm the settings, and then click **Create**.

    To confirm that the virtual machine was created, in the **VMs and Services** workspace, in the **VMs and Services** pane, expand **Clouds**, and then click the private cloud where you deployed the virtual machine. On the **Home** tab, in the **Show** group, click **VMs**. The virtual machine appears in the **VMs** pane.

### <a name="BKMK_Host"></a>Deploying the virtual machine on a host
Use the following procedure to deploy the virtual machine on a host.

1.  On the **Select Host** page, view the ratings, click the host on which you want to deploy the virtual machine, and then click **Next**. The host suggestions are based on a 0-5 star rating. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md). Note the following settings:

    1.  **Expected utilization**�For a virtual machine that is created from a blank hard disk, the expected utilization is based on standard defaults. For a virtual machine that is created from an existing virtual machine, the default settings are based on past performance of the existing virtual machine. VMM updates the host suggestions and ratings in response to modifications that are made to the expected virtual machine utilization.

    2.  **Make this VM highly available**�With this option selected, only hosts that are located in a cluster are available for selection.

    3.  **Details**�Indicates the status of the host, the operating system, and the type and status of virtualization software.

    4.  **Rating Explanation**�Provides an explanation if a host received a zero rating.

    5.  **SAN Explanation** or  **Deployment and Transfer Explanation**�Lists any factors that make a SAN transfer unavailable. VMM does not recognize a virtual machine that is stored on a SAN as available for deployment using SAN transfer if the virtual machine was stored directly in the VMM library when it was created, or if it was added to the VMM library during a library refresh. To avoid this issue, deploy the virtual machine to a host by using a LAN transfer, and then store the virtual machine in the same VMM library, library share, and logical unit number (LUN).

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers (ODX) feature, introduced in Windows Server 2012 R2. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

2.  On the **Configure Settings** page, review the settings for the virtual machine:

    1.  In **Locations**, either accept the default virtual machine path on the host for storing the virtual machine files, or click **Browse** to browse to a different location. Optionally, select the **Add this path to the list of default virtual machine paths on the host** check box.

    2.  In **Operating System Settings**, click **Identity Information**. You can either accept or change the computer name.

    3.  In **Networking**, you can click a network adapter to view the configured network settings.

    4.  In **Machine Resources**, click **Virtual Hard Disk**, then review or modify the settings.

        For example, under **Method to deploy the virtual hard disk to the host**, you can select **Use differencing disk optimizations**.

        Click **Next**.

    > [!TIP]
    > To prevent placement from choosing a different value for these settings, click the pin icon next to the setting. Note that self-service users do not see this option.

3.  On the **Add Properties** page, configure the action to take when the host starts or stops. To prevent the virtual machine from being migrated by Performance and Resource Optimization (PRO) or dynamic optimization, select the **Exclude virtual machine from optimization actions** check box. When you have finished this step, click **Next**.

4.  On the **Summary** page, confirm the settings, and then click **Create**.

### <a name="BKMK_Library"></a>Storing the virtual machine in the library

1.  On the **Select Library Server** page, click the library server that you want to use, and then click **Next**.

2.  On the **Select Path** page, specify the library share location to store the virtual machine. Click **Browse** to select a library share and optional folder location, click **OK**, and then click **Next**.

3.  On the **Summary** page, confirm the settings, and then click **Create**.

    To confirm that the virtual machine was created, in the **Library** workspace, in the **Library** pane, expand **Library Servers**, expand the library server where you stored the virtual machine, and then click **Stored Virtual Machines and Services**. The stored virtual machine appears in the **Physical Library Objects** pane.




