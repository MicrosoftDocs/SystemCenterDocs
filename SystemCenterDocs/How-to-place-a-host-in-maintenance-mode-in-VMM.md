---
title: How to place a host in maintenance mode in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46ee87d0-2823-4a82-a4b1-c67af1fb607f
---
# How to place a host in maintenance mode in VMM
In [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], you can start maintenance mode for a virtual machine host whenever you need to perform maintenance tasks on the physical host, such as applying security updates or replacing hardware on the physical host computer. You can place Hyper\-V hosts and VMware ESX hosts that are managed by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] into maintenance mode.

When you start maintenance mode on a host, you can do one of the following:

-   Place all running virtual machines into a saved state.

-   On a host cluster that is capable of live migration \(including VMware vMotion\), move all highly available virtual machines to other hosts in the cluster.

> [!CAUTION]
> Placing a running virtual machine in a saved state causes a loss of service to any users of that virtual machine.

> [!NOTE]
> For ESX hosts, if the VMware Distributed Resources Scheduler is not configured, all virtual machines on the host must be either manually shut down or moved to another host to successfully start maintenance mode on an ESX host.

When a host is in maintenance mode, the following restrictions are placed on the host:

-   Virtual machines cannot be created on the host.

-   Virtual machines cannot be moved to the host.

-   The host has a zero rating and cannot be selected for placement.

-   The host is excluded from Dynamic Optimization.

> [!NOTE]
> If [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] is integrated with Operations Manager, when a host is placed in maintenance mode in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], Operations Manager also places the host into maintenance mode. In maintenance mode, the Operations Manager agent suppresses alerts, notifications, rules, monitors, automatic responses, state changes, and new alerts.

### To start maintenance mode on a host

1.  In the VMM console, open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Servers**, and then expand **All Hosts**.

4.  In the **Hosts** pane, locate and then click the host that you want to place in maintenance mode.

5.  On the **Host** tab, in the **Host** group, click **Start Maintenance Mode**.

6.  In the **Start Maintenance Mode** dialog box, select either of the following, and then click **OK**.

    -   Move all virtual machines to other hosts in the cluster

    -   Place all running virtual machines into a saved state.

> [!TIP]
> When a host is in maintenance mode, the **Host Status** for the host displays as **In Maintenance Mode** in the **Hosts** pane in the **Fabric** workspace.

### To stop maintenance mode on a host

1.  In the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Servers**, and then expand **All Hosts**.

4.  In the **Hosts** pane, locate and then click the host that you want to bring out of maintenance mode.

5.  On the **Host** tab, in the **Host** group, click **Stop Maintenance Mode**.

> [!IMPORTANT]
> When you bring a host out of maintenance mode, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] does not automatically restart the virtual machines and does not automatically move any migrated virtual machines back on to the host.

## See Also
[Performing maintenance tasks in VMM](./Performing-maintenance-tasks-in-VMM.md)
[Maintaining resources with VMM](./Maintaining-resources-with-VMM.md)
[Managing fabric updates in VMM](./Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](./Managing-fabric-resources-with-VMM.md)


