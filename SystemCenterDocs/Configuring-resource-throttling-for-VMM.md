---
title: Configuring resource throttling for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85fbfd6e-83e7-451c-af2d-eaa02e5e2466
---
# Configuring resource throttling for VMM
[!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] includes resource throttling features such as processor \(CPU\) and memory throttling capabilities. These features can help CPU and memory resources to be allocated more effectively, which then helps virtual machines to run more effectively.

## Processor \(CPU\) throttling
You can set the weight of a virtual processor to provide the processor with a larger or smaller share of CPU cycles, using the following properties:

-   **High, Normal, Low, Custom**—Specifies how the CPU is distributed when contention occurs. Higher priority virtual machines will be allocated CPU first.

-   **Reserve CPU cycles \(%\)—**Specifies the percentage of CPU resources that are associated with one logical processor that should be reserved for the virtual machine. This is useful when a virtual machine runs applications that are particularly CPU\-intensive and you want to ensure a minimal level of CPU resources. A zero setting indicates that no specific CPU percentage is reserved for the virtual machine.

-   **Limit CPU cycles \(%\)**—Specifies that the virtual machine should not consume more that the indicated percentage of one logical processor.

The settings for these properties ensure that virtual machines can be prioritized or deprioritized when CPU resources are overcommitted. For highly intensive workloads, more virtual processors can be added, especially when a physical CPU is close to its upper limit.

## Memory throttling and weight
Memory throttling helps to prioritize or deprioritize access to memory resources in scenarios where memory resources are constrained. When memory usage on a host is high, then the virtual machines with a higher memory priority are allocated memory resources before the virtual machines with a lower priority. If you specify a lower priority, it might prevent a virtual machine from starting when other virtual machines are running and the available memory is low. You can set the memory priority settings and thresholds as follows:

-   **Static**—The amount of static memory that is assigned to a specific virtual machine

-   **Dynamic**—Dynamic memory settings include:

    1.  **Start\-up memory**—The amount of memory that is allocated to the virtual machine when it starts up. It should at least be set to the minimum amount of memory that is required to run the operating system and applications on the virtual machine. Dynamic memory will adjust the memory amount as required.

    2.  **Minimum memory**—The minimum amount of memory that is required for the virtual machine. It allows an idle machine to scale back the memory consumption below the start\-up memory requirement. The available memory can then be used by other virtual machines.

    3.  **Maximum memory**—The memory limit that is allocated to the virtual machine. The default value for[!INCLUDE[win8_server_2](./Token/win8_server_2_md.md)] is 1 TB.

    4.  **Memory Buffer Percentage**—Dynamic memory adds memory to a virtual machine as required, but there is a chance that an application might demand memory more quickly than dynamic memory allocates it. The memory buffer percentage specifies the amount of available memory that will be assigned to the virtual machine if needed. The percentage is based on the amount of memory that is actually needed by the applications and services that run on the virtual machine. It is expressed as a percentage because it changes depending on the virtual machine requirements.

        The percentage is calculated as follows: Amount of memory buffer \= memory needed by the virtual machine\/ \(memory buffer value\/100\). For example, if the memory that is committed to the virtual machine is 1000 MB and the buffer is 20%, then an additional buffer of 20% \(200 MB\) will be allocated for a total of 1200 MB of physical memory allocated to the virtual machine.

    5.  **Memory weight**—The priority that is allocated to a virtual machine when the memory resources are in full use. If you set a high priority value, it will prioritize a virtual machine when the memory resources are allocated. If you set a low priority, a virtual machine might be unable to start if memory resources are insufficient.

For more information, see [How to configure processor and memory throttling for VMM](./How-to-configure-processor-and-memory-throttling-for-VMM.md).

## See Also
[Configuring virtual machine options and settings](./Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](./Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


