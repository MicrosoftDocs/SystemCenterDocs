---
title: How to configure virtual NUMA for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45ae8c7e-93e8-4e4a-b940-4be767e8c794
---
# How to configure virtual NUMA for VMM
With [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] you can configure the virtual Non\-Uniform Memory Access \(NUMA\) features that were introduced in Hyper\-V in [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)]. For more information about these features, see [Deploying virtual NUMA for VMM](Deploying-virtual-NUMA-for-VMM.md). This topic provides the following procedures for configuring virtual NUMA:

1.  [Configuring virtual NUMA settings](#BKMK_VNUMA)—When a new virtual machine is created, Hyper\-V specifies the default settings for virtual NUMA. These settings are in sync with the NUMA topology of the Hyper\-V host. For example, if a host has 16 cores and 64 GB divided evenly between two NUMA nodes, with two NUMA nodes per physical processor socket, then by default, a virtual machine that was created on the host will have the **Maximum processors per virtual NUMA node** property set to 8, the **Maximum virtual NUMA nodes per socket** set to 2, and the **Maximum memory per virtual NUMA node \(MB\)** property set to 32 GB. You can modify the default values as required.

2.  [Configuring virtual NUMA spanning](#BKMK_NUMASPAN)—If virtual NUMA spanning is enabled, then individual virtual NUMA nodes can allocate non\-local memory. If the setting is not enabled, each node uses memory from only one physical NUMA node. Note that whether spanning is enabled or not, virtual nodes can be allocated memory from the same or different underlying host NUMA nodes, based on the physical host topology. NUMA spanning is enabled by default.

## <a name="BKMK_VNUMA"></a>Configuring virtual NUMA settings
Use this procedure to enable and configure virtual NUMA.

#### To configure virtual NUMA settings

1.  In the **Advanced** section of the virtual machine or virtual machine template properties, click **Virtual NUMA**.

2.  In **Maximum processors per virtual NUMA node**, specify the maximum number of virtual processors that belong to the same virtual machine and that can be used concurrently on a virtual NUMA node. Configure this setting to ensure maximum bandwidth. different NUMA virtual machines to use different NUMA nodes. The minimum limit is 1 and the maximum is 32.

3.  In **Maximum memory per virtual NUMA node \(MB\)**, specify the maximum amount of memory \(MB\) that can be allocated to a single virtual NUMA node. The minimum limit is 8 MB and the maximum is 256 GB.

4.  In **Maximum virtual NUMA nodes per socket**, specify the maximum number of virtual NUMA nodes that are allowed on a single socket. The minimum number is 1 and the maximum is 64.

## <a name="BKMK_NUMASPAN"></a>Enable virtual NUMA spanning
Use this procedure to enable or disable virtual NUMA spanning.

#### To enable or disable virtual NUMA spanning

1.  In the **Virtual NUMA** properties page, to enable spanning, select **Allow virtual machine to span hardware NUMA nodes**. Clear the check box to disable spanning.

## See Also
[Deploying virtual NUMA for VMM](Deploying-virtual-NUMA-for-VMM.md)
[Configuring virtual machine options and settings](Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


