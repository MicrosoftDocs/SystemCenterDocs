---
title: Configuring availability options for virtual machines in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8050464b-c28c-44e9-a006-65ab433a2f14
---
# Configuring availability options for virtual machines in VMM
You can use [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] to configure availability options for virtual machines that are deployed on Hyper\-V host clusters. By using [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can configure the following availability options:

-   **Virtual machine priority**: Based on these settings, the host cluster starts or places high\-priority virtual machines before medium\-priority or low\-priority virtual machines. This ensures that the high\-priority virtual machines are allocated memory and other resources first, for better performance. Also, after a node failure, if the high\-priority virtual machines do not have the necessary memory and other resources to start, the lower priority virtual machines will be taken offline to free up resources for the high\-priority virtual machines. Virtual machines that are preempted are restarted later in priority order.

-   **Preferred and possible owners of virtual machines**: These settings influence the placement of virtual machines on the nodes of the host cluster. By default, there are no preferred owners \(there is no preference\), and the possible owners include all server nodes on the cluster.

-   **Availability sets**: When you place multiple virtual machines in an availability set, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will attempt to keep those virtual machines on separate hosts and avoid placing them together on the same host whenever possible. This helps to improve continuity of service. Another way to configure this setting is to use Windows PowerShell commands for failover clustering. In this context, the setting appears in the [Get-ClusterGroup](http://technet.microsoft.com/library/hh847242.aspx) listing and is called **AntiAffinityClassNames**.

The following topics describe how to configure availability options for virtual machines that are being managed with [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]:

-   [How to configure priority in VMM for a virtual machine on a host cluster](../Topic/How-to-configure-priority-in-VMM-for-a-virtual-machine-on-a-host-cluster.md)

-   [How to configure preferred and possible owners for a virtual machine on a host cluster](../Topic/How-to-configure-preferred-and-possible-owners-for-a-virtual-machine-on-a-host-cluster.md)

-   [How to configure availability sets in VMM for virtual machines on a host cluster](../Topic/How-to-configure-availability-sets-in-VMM-for-virtual-machines-on-a-host-cluster.md)

## See Also
[Adding Windows servers as Hyper-V hosts or host clusters in VMM](../Topic/Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)
[Creating a host cluster in VMM from existing Windows servers](../Topic/Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](../Topic/Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Configuring virtual machine options and settings](../Topic/Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](../Topic/Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

