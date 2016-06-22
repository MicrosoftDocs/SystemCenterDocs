---
title: Configuring dynamic optimization and power optimization in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15f08a49-f67e-45b0-87a4-08d82c18a92f
---
# Configuring dynamic optimization and power optimization in VMM
The procedures in this section explain how to configure Dynamic Optimization and Power Optimization in Virtual Machine Manager \(VMM\), and how to run Dynamic Optimization on demand for a host cluster.

VMM can perform load balancing within host clusters that support live migration. Dynamic Optimization migrates virtual machines within a cluster according to settings you enter.

VMM can help to save power in a virtualized environment by turning off hosts when they are not needed and turning the hosts back on when they are needed.

VMM supports Dynamic Optimization and Power Optimization on Hyper\-V host clusters and on host clusters that support live migration in managed VMware ESX. For Power Optimization, the computers must have a baseboard management controller \(BMC\) that enables out\-of\-band management.

## Dynamic Optimization in VMM
During Dynamic Optimization, VMM migrates virtual machines within a host cluster to improve load balancing among hosts and to correct any placement constraint violations for virtual machines.

Dynamic Optimization can be configured on a host group, to migrate virtual machines within host clusters with a specified frequency and aggressiveness. Aggressiveness determines the amount of load imbalance that is required to initiate a migration during Dynamic Optimization. By default, virtual machines are migrated every 10 minutes with medium aggressiveness. When configuring frequency and aggressiveness for Dynamic Optimization, an administrator should factor in the resource cost of additional migrations against the advantages of balancing load among hosts in a host cluster. By default, a host group inherits Dynamic Optimization settings from its parent host group.

Dynamic Optimization can be set up for clusters with two or more nodes. If a host group contains stand\-alone hosts or host clusters that do not support live migration, Dynamic Optimization is not performed on those hosts. Any hosts that are in maintenance mode also are excluded from Dynamic Optimization. In addition, VMM only migrates highly available virtual machines that use shared storage. If a host cluster contains virtual machines that are not highly available, those virtual machines are not migrated during Dynamic Optimization.

On demand Dynamic Optimization also is available for individual host clusters by using the **Optimize Hosts** action in the **VMs and Services** workspace. On demand Dynamic Optimization can be performed without configuring Dynamic Optimization on host groups. After Dynamic Optimization is requested for a host cluster, VMM lists the virtual machines that will be migrated for the administrator's approval.

## Power Optimization in VMM
Power Optimization is an optional feature of Dynamic Optimization, and it is only available when a host group is configured to migrate virtual machines through Dynamic Optimization. Through Power Optimization, VMM helps to save energy by turning off hosts that are not needed to meet resource requirements within a host cluster and turns the hosts back on when they are needed again.

By default, VMM performs power optimization all of the time when the feature is turned on. However, you can schedule the hours and days during the week when power optimization is performed. For example, you might initially schedule power optimization only on weekends, when you anticipate low resource usage on your hosts. After observing the effects of power optimization in your environment, you might increase the hours.

Power Optimization ensures that the cluster maintains a quorum if an active node fails. For clusters created outside VMM and added to VMM, Power Optimization requires more than four nodes. For each additional one or two nodes in a cluster, one node can be powered down. For instance:

-   One node can be powered down for a cluster of five or six nodes.

-   Two nodes can be powered down for a cluster of seven or eight nodes.

-   Three nodes can be powered down for a cluster of nine or ten nodes.

When VMM creates a cluster, it creates a quorum disk and uses that disk as part of the quorum model. For clusters created by VMM, Power Optimization can be set up for clusters of more than three nodes. This means that the number of nodes that can be powered down is as follows:

-   One node can be powered down for a cluster of four or five nodes.

-   Two nodes can be powered down for a cluster of six or seven nodes.

-   Three nodes can be powered down for a cluster of eight or nine nodes.

For more information about quorum configurations, see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](http://technet.microsoft.com/library/jj612870.aspx).

Before turning off a host for Power Optimization, VMM migrates all virtual machines to other hosts in the host cluster. When a host is needed again, VMM turns on the host and then performs Dynamic Optimization to migrate virtual machines and balance load within the host cluster. When Power Optimization is disabled on a host group, or when a scheduled period of Power Optimization ends, the same process occurs with all hosts that were turned off by Power Optimization.

## Resource thresholds for Dynamic Optimization and Power Optimization
The following settings in the host group properties determine the actions that VMM takes on host clusters:

-   Dynamic Optimization settings specify thresholds of resource usage beyond which VMM attempts to migrate virtual machines to improve load balancing. You can specify Dynamic Optimization settings for the following resources: CPU, memory, disk I\/O, and network I\/O.

-   Power Optimization settings specify resource capacity that must be maintained after VMM turns off a host during power optimization. These settings provide a buffer of available resources to ensure that fluctuations in resource usage during normal operations do not result in VMM turning hosts on and off needlessly. Power Optimization settings include CPU, memory, disk space, disk I\/O, and network I\/O.

When Power Optimization is enabled on a host group, Dynamic Optimization and Power Optimization are performed in concert. Hosts that VMM has turned off to conserve energy can be turned on to balance load or to meet virtual machine requirements.

For more information about configuring Dynamic Optimization levels and placement levels for a host group, see [How to configure Dynamic Optimization and Power Optimization in VMM](How-to-configure-Dynamic-Optimization-and-Power-Optimization-in-VMM.md).

## Prerequisites
To use Dynamic Optimization and Power Optimization, ensure that the following requirements are met:

-   To use Dynamic Optimization, VMM must be managing a host cluster that supports live migration. For information about Hyper\-V host clusters, see [Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md). For information about VMware ESX hosts, see [Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md).

    > [!NOTE]
    > You can configure Dynamic Optimization and Power Optimization on any host group. However, the settings will not have any effect unless the host group contains a host cluster.

-   To use Power Optimization, the host computers must have a BMC that enables out\-of\-band management. For more information about the BMC requirements, see [Configure computer BMC settings for bare-metal deployment ](Configure-computer-BMC-settings-for-bare-metal-deployment.md).

-   To view Dynamic Optimization and Power Optimization in action, you must deploy and run virtual machines on the host cluster. For more information, see [Overview: creating and deploying virtual machines in VMM](Overview--creating-and-deploying-virtual-machines-in-VMM.md).

## In this section
Use the procedures in this section to perform the following tasks.

|Procedure|Description|
|-------------|---------------|
|[How to configure dynamic optimization and power optimization in VMM](How-to-configure-Dynamic-Optimization-and-Power-Optimization-in-VMM.md)|Describes how to configure Dynamic Optimization and Power Optimization for a host group.|
|[How to run Dynamic Optimization on a host cluster in VMM](How-to-run-Dynamic-Optimization-on-a-host-cluster-in-VMM.md)|Describes how to initiate Dynamic Optimization on demand within a host cluster by using the **Optimize Hosts** action in the **Fabric** workspace.|

## See Also
[Managing host groups in VMM](Managing-host-groups-in-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


