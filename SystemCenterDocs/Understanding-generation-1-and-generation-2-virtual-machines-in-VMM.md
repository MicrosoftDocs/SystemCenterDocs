---
title: Understanding generation 1 and generation 2 virtual machines in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1723599e-af0e-4f7d-a932-9f23d493a9ff
---
# Understanding generation 1 and generation 2 virtual machines in VMM
In [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], on a host running [!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)], you can create and manage two types of virtual machines. The two types include the newer type supported in Hyper\-V as of [!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)], called “generation 2 virtual machines.” Before generation 2 virtual machines existed, virtual machines were all of one type, which are now referred to as “generation 1 virtual machines.” For more information, see [Generation 2 Virtual Machine Overview](http://technet.microsoft.com/library/dn282285.aspx).

A virtual machine must be either a generation 1 virtual machine or a generation 2 virtual machine.  In [!INCLUDE[vmm12short](Token/vmm12short_md.md)], you can use the wizards and property sheets to choose options for either a generation 1 virtual machine or a generation 2 virtual machine, but not both together.

You can specify generation 1 or generation 2 virtual machines in VM templates that you add to services in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]. A service can include both generation 1 virtual machines and generation 2 virtual machines.

This topic contains the following sections:

-   [Host requirements for generation 2 virtual machines](#BKMK_Hostreq)

-   [Customizing the startup order for a generation 2 virtual machine](#BKMK_Customstart)

-   [Creating a virtual machine or virtual machine template and specifying the generation](#BKMK_Specgen)

## <a name="BKMK_Hostreq"></a>Host requirements for generation 2 virtual machines
Generation 2 virtual machines can only run on a host with a host operating system that supports them. [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)] and[!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)] support generation 2 virtual machines, and [!INCLUDE[vmm12short](Token/vmm12short_md.md)] will avoid placing generation 2 virtual machines on hosts that are running earlier operating systems. For example, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] will avoid placing a generation 2 virtual machine on a host running [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)].

## <a name="BKMK_Customstart"></a>Customizing the startup order for a generation 2 virtual machine
Because of underlying differences between generation 1 and generation 2 virtual machines, the startup order \(boot order\) for different devices \(such as a hard disk or CD\) is not handled the same way in the two generations. To customize the startup order for a generation 2 virtual machine in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], you must use a Windows PowerShell command that specifies the first boot device, rather than an ordered list of boot devices. The following list outlines the differences in the methods for customizing the startup order.

-   **Customizing the startup order for generation 1 virtual machines**

    One way to customize the startup order for generation 1 virtual machines is by using the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console. To use the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console, in the wizards for adding a hardware profile, virtual machine, or virtual machine template, on the page where you configure hardware settings, under **Advanced**, in the **Firmware** section, you can modify the order of items in the **Startup order** list. Another way to customize the startup order is to use Windows PowerShell commands with the **BootOrder** parameter, which is described in more detail in TechNet topics for cmdlets such as [Set-SCVirtualMachine](http://technet.microsoft.com/library/jj654500.aspx), [Set-SCVMTemplate](http://technet.microsoft.com/library/jj654252.aspx), or [Set-SCHardwareProfile](http://technet.microsoft.com/library/jj647740.aspx).

-   **Customizing the startup order for generation 2 virtual machines**

    To customize the first boot device for generation 2 virtual machines, you must use Windows PowerShell commands with the **FirstBootDevice** parameter. By default, the first boot device is set to a virtual hard disk—either the virtual hard disk marked as **Contains the operating system for the virtual machine**, or the only virtual hard disk, if the virtual machine has only one.

    The **FirstBootDevice** parameter is described in more detail in TechNet topics for cmdlets, such as [Set-SCVirtualMachine](http://technet.microsoft.com/library/jj654500.aspx), [Set-SCVMTemplate](http://technet.microsoft.com/library/jj654252.aspx), or [Set-SCHardwareProfile](http://technet.microsoft.com/library/jj647740.aspx). For example, you could run the following command to configure an existing virtual machine template called **Generation2template** so that the first boot device is the first network adapter. This command is based on the assumption that the network adapter supports the Pre\-Boot Execution Environment \(PXE\):

    ```
    Set-SCVMTemplate -Template "Generation2template" –FirstBootDevice "NIC,0"
    ```

## <a name="BKMK_Specgen"></a>Creating a virtual machine or virtual machine template and specifying the generation
When you use a [!INCLUDE[vmm12short](Token/vmm12short_md.md)] wizard to create a new virtual machine or virtual machine template, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] responds to your selections as follows:

-   If you use a virtual hard disk in .vhd format \(the older format\) as the starting point for a virtual machine or virtual machine template, it automatically becomes generation 1, because generation 2 virtual machines support only the .vhdx format. In this situation, you do not see the **Generation** list box on the second page of the wizard, and you cannot select the generation.

-   If you use a virtual hard disk in .vhdx format \(the newer format\) as the starting point for the virtual machine or virtual machine template, when you reach the second page of the wizard \(the **Identity** page\), you have two choices for the virtual machine or virtual machine template: **Generation 1** or **Generation 2**. By default, **Generation 1** is selected.

    This guideline also applies if you create a virtual machine and choose **Create the new virtual machine with a blank virtual hard disk**. With this option, the blank disk uses the .vhdx format.

-   If you use an existing virtual machine or virtual machine template as the starting point for a new virtual machine or virtual machine template, the generation is determined by the existing virtual machine or virtual machine template.

-   If you create a hardware profile \(to make it easier to consistently apply the same hardware settings to multiple virtual machines or virtual machine templates\), on the first page of the New Hardware Profile Wizard, you must choose between **Generation 1** or **Generation 2**. By default, **Generation 1** is selected.

    When you later incorporate the hardware profile into a virtual machine or virtual machine template, in the respective wizard, the generation of the virtual machine or virtual machine template is determined on the first or second page \(as described earlier in this list\). Then, on the wizard page that contains the **Hardware profile** list box, the only hardware profiles that appear are those of the same generation as the virtual machine or virtual machine template that you are creating.

After the generation has been determined for a hardware profile, virtual machine, or virtual machine template, as you progress through a wizard, the capabilities that do not apply to that generation are either absent or they appear dimmed. For example, if you select **Generation 1** on the **Identity** page, when you advance to the **Configure Hardware** page, under **Bus Configuration**, **IDE Devices** appears. IDE devices are found only in generation 1 virtual machines. In contrast, if you select **Generation 2** on the **Identity** page, when you advance to the **Configure Hardware** page, under **Bus Configuration**, **IDE Devices** does not appear. Instead, for the **SCSI Adapters** that appear, attached devices are shown, which reflects the unique capability in generation 2 virtual machines to boot from a SCSI\-attached virtual hard disk.

Similarly, with a Windows PowerShell command, if you try to combine the unique capabilities of both generations into one virtual machine or virtual machine template, the command does not succeed, and an error message is displayed. Also, if you try to modify an existing virtual machine or virtual machine template by adding options from the other generation, the command does not succeed, and an error message is displayed. For more information about the unique capabilities in generation 2 virtual machines, see [Generation 2 Virtual Machine Overview](http://technet.microsoft.com/library/dn282285.aspx).

## See Also
[Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md)
[How to create a virtual machine template](How-to-create-a-virtual-machine-template.md)
[How to create a hardware profile](How-to-create-a-hardware-profile.md)
[Generation 2 Virtual Machine Overview](http://technet.microsoft.com/library/dn282285.aspx)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


