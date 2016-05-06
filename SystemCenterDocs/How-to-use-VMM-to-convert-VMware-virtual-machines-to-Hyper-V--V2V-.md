---
title: How to use VMM to convert VMware virtual machines to Hyper-V (V2V)
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4deab84b-42c2-43c7-b528-3420925cbdcd
---
# How to use VMM to convert VMware virtual machines to Hyper-V (V2V)
You can use the following procedure to convert a VMware virtual machine to a Hyper\-V virtual machine through the virtual\-to\-virtual \(V2V\) machine conversion process in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. The source virtual machine can be stored in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library or managed by a VMware ESX host.

> [!NOTE]
> You can also perform V2V conversions with Microsoft Virtual Machine Converter \(MVMC\). For more information, see [Microsoft Virtual Machine Converter 3.0](http://technet.microsoft.com/library/dn873998.aspx).

**Before you begin**

Before you begin, there are several things you need to be aware of concerning V2V conversions:

-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not support converting VMware Workstations.

-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not support converting VMware virtual machines with virtual hard disks that are connected to an integrated drive electronics \(IDE\) bus.

-   Online V2V conversions are not supported. This means VMware virtual machines must be offline \(powered off\).

-   You must stop any anti\-virus applications that are running.

-   You must uninstall VMware Tools on the guest operating system of the virtual machine. For information about VMWare Tools, see [Overview of VMware Tools](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=340).

[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)] supports the V2V machine conversion of virtual machines that are running on the following versions of VMware ESX:

-   ESX\/ESXi 4.1

-   ESXi 5.1

### To convert VMware virtual machines to Hyper\-V using the Convert Virtual Machine Wizard

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Create** group, click the **Create Virtual Machine** drop\-down arrow, and then click **Convert Virtual Machine**.

    The Convert Virtual Machine Wizard opens.

3.  On the **Select Source** page, next to the **Select the virtual machine that you would like to convert** box, click **Browse**.

4.  In the **Select Virtual Machine Source** dialog box, click the VMware virtual machine that you want to convert, and then click **OK**.

    > [!TIP]
    > Verify that the **Virtualization Platform** column indicates **VMware ESX Server**.

5.  On the **Select Source** page, click **Next**.

6.  On the **Specify Virtual Machine Identity** page, either keep or change the virtual machine name, enter an optional description, and then click **Next**.

    > [!NOTE]
    > The virtual machine name identifies the virtual machine to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. The name does not have to match the computer name of the virtual machine. However, to avoid confusion, we recommend that you use the same name as the computer name.

7.  On the **Virtual Machine Configuration** page, configure the number of processors and assign the amount of memory in megabytes or gigabytes, and then click **Next**.

8.  On the **Select Host** page, select a Hyper\-V host for placement, and then click **Next**.

9. On the **Select Path** page, do the following, and then click **Next**:

    1.  In the **Storage location** box, configure the storage location on the host for virtual machine files. By default, the default virtual machine paths on the target host are listed. To select a different location, click **Browse**, click a folder, and then click **OK**.

        > [!NOTE]
        > As a best practice, do not specify a path that is on the same drive as the operating system files.

    2.  To add the path to the list of storage locations on the virtual machine host, select the **Add this path to the list of default storage locations on the host** check box.

10. On the **Select Networks** page, select the logical network, the virtual network, and the virtual LAN \(VLAN\), if applicable, to use for the virtual machine, and then click **Next**.

    > [!NOTE]
    > The list of available logical networks, virtual networks, and VLANs matches what is configured on the host physical network adapters.

11. On the **Add Properties** page, configure the settings that you want, and then click **Next**.

12. On the **Summary** page, review the settings. Optionally, select the **Start the virtual machine after deploying it** check box. To start the conversion process, click **Create**.

    The **Jobs** dialog box appears to indicate the job status. Verify that the job has a status of **Completed**, and then close the dialog box.

13. To verify that the virtual machine was converted, do the following:

    1.  In the **VMs and Services** workspace, locate and then click the Hyper\-V host which you selected during placement.

    2.  On the **Home** tab, in the **Show** group, click **VMs**.

    3.  In the **VMs** pane, verify that the virtual machine appears.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](../Topic/Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)

