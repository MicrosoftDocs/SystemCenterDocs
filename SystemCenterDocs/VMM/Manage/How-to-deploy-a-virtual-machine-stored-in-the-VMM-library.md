---
title: How to deploy a virtual machine stored in the VMM library
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c679edf5-58c8-4518-9716-32428bf8ca78
---
# How to deploy a virtual machine stored in the VMM library
Use the following procedure to deploy a virtual machine that is stored in the [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] library. For information about creating a virtual machine and storing it in the library, see [Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md).

### To deploy a virtual machine stored in the VMM library

1.  In the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console, in the **Library** workspace, in the navigation pane, navigate to the library server on which the virtual machine is stored, and then click **Stored Virtual Machines and Services**.

2.  In the results pane, select the virtual machine.

3.  On the **Virtual Machine** tab, in the **Actions** group, click **Deploy**.

    The Deploy Virtual Machine Wizard opens.

4.  On the **Select Host** page, select a host on which to deploy the virtual machine. In the list of hosts, all available hosts are given a rating of 0–5 stars, based on their suitability to host the virtual machine. The host rating levels are recommendations. You can select any host that has the required disk space, even if the host has a zero host rating. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md).

    **Network optimization** If a host has network optimization enabled, a green check mark appears in the **Network Optimization** column. Network optimization capabilities apply to Hyper\-V hosts running Windows Server 2008 R2. For information about network optimization and the hardware that supports it, see the Windows Server 2008 R2 topics, [Using Virtual Machine Chimney](http://technet.microsoft.com/library/gg162677.aspx) and [Using Virtual Machine Queue](http://technet.microsoft.com/library/gg162704.aspx).

    **Highly available virtual machines** To make a virtual machine a highly available virtual machine \(HAVM\), you can migrate the virtual machine to a host that is in a host cluster, even if the virtual machine has not been configured as highly available. The wizard also enables you to migrate a highly available virtual machine to a stand\-alone host. Because of the resulting change to the virtual machine’s highly available setting, either of these actions requires confirmation.

    > [!NOTE]
    > For more information about environmental factors and settings that affect virtual machine placement in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md).

    -   To get additional information about the host, select the host, and view the tabs in the **Details** area.

        **Details**—Indicates the status of the host, the operating system, and the type and status of virtualization software. Lists the virtual machines on the host.

        **Rating Explanation**—Lists the factors that resulted in a rating, if the host received a zero rating.

        **SAN Explanation** or **Deployment and Transfer Explanation**— Lists factors that make a SAN transfer unavailable.

        In addition, the **Deployment and Transfer Explanation** tab provides an explanation if fast file copy cannot be used. Fast file copy is based on the Windows Offloaded Data Transfers \(ODX\) feature, introduced in [!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)]. For information about ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).

    -   To change the host rating criteria for the current virtual machine, click **Customize Ratings**. You can change the placement goal and the relative importance that is placed on the availability of CPU, memory, disk I\/O capacity, and network capacity for the current virtual machine. For more information, see [Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md).

5.  On the **Select Path** page, do the following:

    1.  In **Save Path**, click **Browse**, navigate to the folder in which you want to store the configuration files for the virtual machine, and then click **OK**.

    2.  If you selected a path other than a default virtual machine path, and you want to store other virtual machines on that path, select the **Add this path to the list of host default paths** check box to add the path to the default paths on the host.

    3.  If SAN transfers are enabled for this deployment, by default, the virtual machine is transferred to the host over the storage area network \(SAN\). If you do not want to perform a SAN transfer, select the **Transfer over the network even if a SAN transfer is available** check box. If SAN transfers are not available for this deployment, this option is not available.

6.  On the **Select Networks** page, select the network settings for the virtual machine to use.

7.  On the **Summary** page, review your settings. To change settings, click **Previous**.

    To start the virtual machine after it is deployed, select the **Start the virtual machine immediately after deploying it to the host** check box.

8.  To begin deploying the virtual machine, click **Deploy**.

    To review the progress and results of the operation, open the **Jobs** workspace. By default, the workspace opens when the wizard closes. To view this workspace at any time, click **Jobs** on the taskbar in the results pane of the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console.

## See Also
[Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)


