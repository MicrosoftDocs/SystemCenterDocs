---
title: Deploying virtual NUMA for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59686634-a388-44cc-ac3b-bd14d7866243
---
# Deploying virtual NUMA for VMM
With Virtual Machine Manager (VMM) you can configure, deploy, and manage the virtual Non-Uniform Memory Access (NUMA) features that were introduced in Hyper-V in Windows Server 2012.

NUMA is a memory architecture that is used in multiprocessor systems, where the time that is required for a processor to access memory depends on the location of the memory relative to the processor. On a NUMA system, a processor can access the local memory (the memory that is directly attached to the processor) faster than the non-local memory (the memory that is attached to another processor). NUMA attempts to close the gap between the speed of processors and the memory that they use. To do so, NUMA provides separate memory on a per-processor basis, thus This helps to avoid the performance degradation that occurs when multiple processors try to access the same memory. Each block of dedicated memory is known as a NUMA node.

## NUMA features in Hyper-V
As of Windows Server 2012, Hyper-V supported running on a host system with up to 320 logical processors. The number of virtual processors that can be configured in a virtual machine depends on the number of processors on the physical computers.  For example, to configure a virtual machine with the maximum of 64 virtual processors, you must be running Hyper-V on a virtualization host that has 64 or more logical processors. In order to support this scalability, Hyper-V provides virtual NUMA, a synthetic NUMA-like environment for virtual machines. Virtual processors and guest memory are grouped into virtual NUMA nodes, and the virtual machine presents a topology to the guest operating system based on the underlying physical topology.

By default, when a virtual machine is created, Hyper-V examines the underlying physical topology and automatically configures the virtual NUMA topology with optimal settings, based on a number of factors, which include the number of logical processors and the amount of memory per NUMA node.

Virtual NUMA enables the deployment of larger and more mission-critical workloads that can be run without significant performance degradation in a virtualized environment, when compared to running non-virtualized computers with physical NUMA hardware. When a new virtual machine is created, by default Hyper-V uses values for the guest settings that are in sync with the Hyper-V host NUMA topology. For example, if a host has 16 cores and 64 GB divided evenly between two NUMA nodes with two NUMA nodes per physical processor socket, then a virtual machine that is created on the host with 16 virtual processors will have the maximum number of processors per node setting set to eight, maximum nodes per socket set to two, and maximum memory per node set to 32 GB.

In addition, NUMA spanning can be enabled or disabled. With spanning enabled, individual virtual NUMA nodes can allocate non-local memory, and an administrator can deploy a virtual machine that has more virtual processors per virtual NUMA node than the number of processors that are available on the underlying hardware NUMA node on the Hyper-V host. NUMA spanning for a virtual machine does incur a performance cost because virtual machines access memory on non-local NUMA nodes.

For information about how to configure virtual NUMA, see [How to configure virtual NUMA for VMM](How-to-configure-virtual-NUMA-for-VMM.md).

