---
title: How to create a physical computer profile to provision hosts or host cluster nodes from bare metal in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80835c9e-8753-4919-897f-f115c4d3a535
---
# How to create a physical computer profile to provision hosts or host cluster nodes from bare metal in VMM
In [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)], you can use physical computer profiles to provision bare\-metal computers into Hyper\-V hosts or host cluster nodes.

Before you begin this procedure, be sure to review the prerequisites for the profile in [Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

### To create a physical computer profile for a host or host cluster node

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create** > **Physical Computer Profile**.

    The New Physical Computer Profiles Wizard opens.

3.  On the **Profile Description** page, type a name and optional description.

    Click  **VM Host**.

4.  On the **OS Image** page, do the following:

    1.  Click **Browse**, click the generalized virtual hard disk file that you added to the library share, and then click **OK**.

        > [!IMPORTANT]
        > Requirements for the virtual hard disk are listed in [Profile requirements (for the physical computer profile)](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_profile) in "Prerequisites: Creating hosts or host clusters from bare metal in VMM."

    2.  By default, if the disk type is dynamic, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically converts the disk to a fixed disk type during deployment. We strongly recommend that for production servers, you use a fixed disk type to increase performance and to help protect user data. However, if you do not want to use a fixed disk, select **Do not convert the virtual hard disk type to fixed during deployment**.

    3.  Click **Next** to continue.

5.  On the **Hardware Configuration** page, configure the options listed in the following table, and then click **Next**.

    |||
    |-|-|
    |**Physical  NIC**<br /><br />\(under **Network Adapters**\)|-   If you've already configured logical networks or logical switches in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you can include those configurations in the physical computer profile. See the requirements in [Profile requirements (for the physical computer profile)](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_profile) in "Prerequisites: Creating hosts or host clusters from bare metal in VMM."<br />-   To add a network adapter, use the **Add** button and select the appropriate option.<br />-   To remove an adapter, select it, and click the **Remove** button.<br />-   To provide a Consistent Device Naming \(CDN\) name for the selected adapter, click **Connectivity Properties**.<br />-   To choose between DHCP and static IP addressing \(which requires a logical network that you specify\), click **IP Configuration**. \(If you have specified that a logical switch will be applied to the physical NIC, the **IP Configuration** options will be disabled.\)<br />    For information about logical networks and IP address pools, see[Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md).|
    |**Disk**<br /><br />\(under **Disk and Partitions**\)|Specify the partitioning scheme for the first disk. You can select either of the following options:<br /><br />-   **Master Boot Record \(MBR\)** for computers that use the BIOS.<br />-   **GUID Partition Table \(GPT\)** for computers that use Extensible Firmware Interface \(EFI\).<br /><br />Under **Disk**, click the default partition name **OS** and configure options in the **Partition information** pane:<br /><br />-   Volume label<br />-   How to use free disk space<br />-   Whether this is the boot partition **Note:**     During deployment, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically creates a system partition on the same disk where the boot partition is located.<br /><br />To add a new disk or partition, use the **Add** button and then configure the settings for the new disk or partition.|
    |**Driver filter**<br /><br />\(under **Driver Options**\)|You can filter the driver files that will be applied to the operating system during deployment:<br /><br />-   **Filter drivers with matching PnP IDs**. By default, drivers that match the Plug and Play IDs on the target physical computer are used.<br />-   **Filter drivers with all matching tags specified below**. If you select this option, enter the tags that you want to use for filtering, separated by semicolons, or click **Select** to view and assign the available tags. If you click **New Tag**, you can change the name of the tag after you click **OK**. **Note:** For information about adding tags to driver files in the library, see [How to add driver files to the VMM library](How-to-add-driver-files-to-the-VMM-library.md).|

6.  On the **OS Configuration** page, configure the options listed in the following table, and then click **Next**.

    |||
    |-|-|
    |**Domain**|1.  Specify the domain that the computer should join. For example, type **contoso.com**.<br />2.  Click **Browse**, and then select the Run As account that will be used to join the computer to the domain. For example, you might have a Run As account called **Add Physical Computer**.|
    |**Admin Password**|Type the password that you want to assign to the local Administrator account on the physical computer. You cannot specify a blank password.|
    |**Identity Information**|Optionally, provide a **Full name** and **Organization name**.|
    |**Product Key**|Enter the product key. For multiple computers, you must use a Volume Licensing key. **Note:** If you do not enter a product key, the standard activation grace period applies.|
    |**Time Zone**|Select the time zone for the computer.|
    |**Answer File**<br /><br />\(under **Scripts**\)|To use an answer file to specify additional settings, click **Browse**, click the Unattend.xml file that you want to use, and then click **OK**. **Note:** When you deploy hosts or host clusters from bare metal, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically performs the following \(no answer file or script needed\):<ul><li>**For Hyper\-V hosts**: installs the Hyper\-V role.</li><li>**For Hyper\-V host cluster nodes**: installs the Hyper\-V role, failover cluster feature, and Multipath I\/O \(MPIO\) feature.</li></ul>|
    |**\[GUIRunOnce\] Commands**<br /><br />\(under **Scripts**\)|You can specify one or more commands to run the first time a user signs in to the computer. Type each command and then click **Add**. You can also change the order of commands \(**Move Up** and **Move Down**\) and remove commands.|
    |**Post\-deployment script** \(under **Post\-Deployment Scripts**\)|If you click the **Add Script** button near the top of the page, an entry for a **Post\-deployment script** is added under **Post\-Deployment Scripts**. Then, in the results pane, you can specify the **Executable program**, the **Parameters**, and other options for running the script command. If you add multiple script commands, at the top of the results pane for each one, you can specify the **Deployment order**.<br /><br />To specify additional options such as the failure policy, click the **Advanced** button.<br /><br />See the entry for **Answer File**, earlier in this table, for a list of roles and features that [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] installs automatically \(no script needed\).<br /><br />For example, after placing a script called **EnableRDS.ps1** in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library in a folder called **RemoteDesktop.cr**, you could specify:<br /><br />-   **Executable program**: `PowerShell.exe`<br />    \(as a best practice, add the full path before the executable name\)<br />-   **Parameters**: `-ExecutionPolicy Bypass -Command "EnableRDS.ps1"`<br />-   **Script resource package**: `RemoteDesktop.cr`|

7.  As needed, in the **Host Settings** page, specify a path on the host where files associated with virtual machines should be placed, click **Add**, and then click **Next**. Do not specify a location on drive C, which is not available for placement. If you do not specify a path, placement determines the most suitable location.

    > [!NOTE]
    > You can accept the default path, specify a new path, or change the path after you deploy the host.

8.  On the **Summary** page, confirm the settings, and then click **Finish**.

    Depending on settings, the **Jobs** dialog box may appear. Make sure that the job status is **Completed**, and then close the dialog box.

9. To verify that the physical computer profile was created, in the **Library** pane, expand **Profiles**, and then click **Physical Computer Profiles**.

    The new physical computer profile appears in the **Profiles** pane.

## See Also
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Managing infrastructure resources with VMM](Managing-infrastructure-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


