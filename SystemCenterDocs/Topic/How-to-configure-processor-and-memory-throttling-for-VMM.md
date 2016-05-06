---
title: How to configure processor and memory throttling for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9dce4d4a-949f-4e5f-a56e-715dfc2fd535
---
# How to configure processor and memory throttling for VMM
[!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] provides processor throttling \(CPU\) and memory throttling capabilities. You can set the throttling values when you configure a virtual machine by using the Create Virtual Machine Wizard, on the property sheet of an existing virtual machine, or on a virtual machine template. This topic describes how to configure processor and memory throttling, and memory weight.

For more information about processor and memory throttling, see [Configuring resource throttling for VMM](../Topic/Configuring-resource-throttling-for-VMM.md).

## <a name="BKMK_CPUThrottle"></a>To configure processor throttling

1.  In the **Advanced** section of the virtual machine or of the virtual machine template properties, click **CPU Priority**.

2.  Select a priority value for the virtual machine. These values specify how the CPU resources are balanced between virtual machine, and correspond to the relative weight value in Hyper\-V:

    -   High—Relative weight value of 200

    -   Normal—Relative weight value of 100

    -   Low—Relative weight value of 50

    -   Custom—Relative weight values that are supported are between 1 and 10000

3.  In **Reserve CPU cycles \(%\)**, specify the percentage of the CPU resources on one logical processor that should be reserved for a virtual machine. This is useful when a virtual machine runs applications that are particularly CPU\-intensive, and you want to ensure a minimal level of CPU resources. A zero setting indicates that no specific CPU percentage is reserved.

4.  In **Limit CPU cycles \(%\)**, specify the maximum percentage of the CPU resources on one logical processor that the virtual machine should consume. The virtual machine will not be allocated more than this percentage.

## <a name="BKMK_MemoryThrottle"></a>To configure memory throttling

1.  In the **General** section of the virtual machine or of the virtual machine template properties, click **Memory**.

2.  Select **Static** to specify that a fixed amount of memory should be assigned to a virtual machine.

3.  Select **Dynamic** to specify the dynamic memory settings for a virtual machine, as follows:

    1.  In **Startup memory**, specify the amount of memory that is allocated to the virtual machine when it starts up. The memory value should be set at least to the minimum amount of memory that is required for the virtual machine operating system and applications to run.

    2.  In **Minimum memory**, specify an amount of memory that allows an idle virtual machine to scale back the memory consumption below the startup memory requirement. This makes more memory available for use by other virtual machines.

    3.  In **Maximum memory**, specify the maximum amount of memory that is allocated to a virtual machine. The default setting for [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)] is 1 TB.

    4.  In **Memory buffer percentage** specify the amount of available memory that will be assigned to a virtual machine if the need arises. The percentage should be based on the amount of memory that is actually needed by the applications and services that run on the virtual machine. The memory buffer percentage should be calculated as follows: Amount of memory buffer \= memory that is needed by the virtual machine\/ \(memory buffer value\/100\). For example, if the memory that is committed to the virtual machine is 1000 MB and the buffer is 20%, then an additional buffer of 20% \(200 MB\) will be allocated for a total of 1200 MB of physical memory allocated to the virtual machine.

## <a name="BKMK_Weight"></a>To configure memory weight

1.  In the **Advanced** section of the virtual machine or of the virtual machine template properties, click **Memory Weight**.

2.  Configure the priority that is used to allocate memory to a virtual machine when memory resources are in high usage. If you specify a low priority, the virtual machine might not be available to start when the memory resources are not sufficient.

## See Also
[Configuring resource throttling for VMM](../Topic/Configuring-resource-throttling-for-VMM.md)
[Configuring virtual machine options and settings](../Topic/Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](../Topic/Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

