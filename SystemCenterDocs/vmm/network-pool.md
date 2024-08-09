---
ms.assetid: a0d8b08f-b44f-476e-a530-493378c2e4da
title: Set up static IP address pools in the VMM fabric
description: This article describes how to set up IP address pools in the VMM fabric
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 08/09/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2
---

# Set up static IP address pools in the VMM fabric



This article describes how to set up static IP address pools for logical and VM networks in the System Center Virtual Machine Manager (VMM) networking fabric.

>[!NOTE]
> While creating a static IP address pool in VMM, don't use the IP address range (that is managed by the pool) outside of VMM, in the same environment.

When you set up the logical network, you'll need to configure a static IP address pool if you're not using DHCP. In some circumstances you'll need to create IP address pools on the logical network only, and in others you'll need to create the pool on both the logical and VM networks:

- **Pool on logical and VM network**: If you configure your logical network for network virtualization, you'll need to create IP address pools on the logical network and the VM network.
- **Pool on logical network only**: If you're using VLAN or no isolation, you can use DHCP or create IP address pools on the logical network only. They'll automatically become available on the VM network.
- **Imported address pools**: If you're using external networks through a vendor console, your IP address pools will be imported from the vendor, and you don't need to create them in VMM.


## Create a static address pool for a logical network

1. In **Logical Networks and IP Pools**, select the logical network > **Home** > **Create** > **Create IP Pool**.
2. In **Create Static IP Address Pool Wizard** > **Name**, specify a name and description. Ensure that the correct logical network is indicated.
3. In **Network Site**, select to use an existing site and select the IP subnet or create a new site.

	- For an existing site, select the site and IP subnet from which to create the pool.
	- For a new site, specify the site name, IP subnet to assign to the site, and VLAN information if relevant. Select the host groups that can access this site and the logical network.
4. If you're using network virtualization, you can use the pool to support multicasting or broadcasting. To do this, select **Create a multicast IP address pool** and select the IP subnet you want to use. To use multicasting or broadcasting, ensure that:

	- The logical network must have network virtualization enabled.
	- The IP protocol setting for the VM network must match the IP protocol settings for the underlying logical network. You can't view the protocol setting in the VMM console after you've created it. You'll need to run **Get-SCVMMNEtwork -Name \<VM network name\> | Format -List Name, Isolation Type, PoolType** to see it.
	- After you've configured this feature, multicast and broadcast packets on the VM network will use the IP addresses from the multicast IP address pool. Each subnet in the VM network will consume one IP address from the multicast pool.

5. In **IP address range**, enter the start and end address for the pool. They must be contained within the subnet. In **VIPs and reserved IP addresses**, specify the IP address range you want to reserve for VIPs. VIPS are used during the deployment of a service in a load-balanced service tier. VMM automatically assigns a VIP to the load balancer from the reserved VIP address range.
6. In **Gateway**, select **Insert** if you want to specify one or more default gateways and the metric. The default gateway address must be in the same subnet range as the IP address pool but doesn't need to be part of the pool.
7. In **DNS**, specify DNS information, including DNS servers, the default DNS suffix for the connection, and the list of DNS search suffixes.
8. In **WINS**, select **Insert** if you want to enter the IP address of a WINS server. You can also select whether to enable NetBIOS over TCP/IP. This isn't recommended if the address range is made up of public addresses.
9. In **Summary**, verify the settings and select **Finish**. When the job shows as **Completed**, verify the pool in **Logical Networks and IP Pools**.

## Set up an IP address pool on a VM network

1. Select **VMs and Services** > **VM Networks**  > **Home** > **Show** > **VM Networks** > **VM Network**.
2. In  **VM Networks and IP Pools**, select the VM network > **Create** > **Create IP Pool**.
2. In **Create Static IP Address Pool Wizard** > **Name**, specify a name and description. Ensure that the correct logical network is indicated. Ensure the correct VM network and subnet is selected.
3. In **IP address range**, enter the start and end addresses for the pool. You can create multiple IP address pools in a subnet but the ranges mustn't overlap. In **Reserved IP addresses**, specify any range you want to reserve for other purposes.
6. In **Gateway**, select **Insert** if you want to specify one or more default gateways and the metric. The default gateway address must be in the same subnet range as the IP address pool but doesn't need to be part of the pool.
7. In **DNS**, specify DNS information, including DNS servers, the default DNS suffix for the connection, and the list of DNS search suffixes. For virtual machines that will join an Active Directory domain, we recommend that you use Group Policy to set the primary DNS suffix. This will ensure that when a Windows-based virtual machine is set to register its IP addresses with the primary DNS suffix, a Windows-based DNS server will register the IP address dynamically. Additionally, the use of Group Policy enables you to have an IP address pool that spans multiple domains. In this case, you would not want to specify a single primary DNS suffix.
8. In **WINS**, select **Insert** if you want to enter the IP address of a WINS server. You can also select whether to enable NetBIOS over TCP/IP. This isn't recommended if the address range is made up of public addresses.
9. In **Summary**, verify the settings and select **Finish**. When the job shows as **Completed**, verify the pool in **Logical Networks and IP Pools**.


### Release inactive addresses from the static address pool

You can release inactive addresses. When you do, VMM returns the address to the static IP pool, or MAC address pool and considers it available for reassignment. An address is considered inactive if:

- A host that was assigned a static IP address through the bare-metal deployment process is removed from VMM management. When you remove the host, any IP and MAC addresses that were statically assigned to virtual machines on the host are also marked as inactive.
- A virtual machine goes into a missing state because it was removed outside VMM.

1. Release the IP addresses:

	- To release addresses in a pool in a logical network, select **Logical Networks and IP Pools**, expand the logical network, and select the IP address pool.
	- To release addresses in a pool in a VM network, select **Logical Networks and IP Pools**, expand the VM network, and select the IP address pool.
2. Select **Home** > **Properties** > **Inactive addresses**, and select the inactive IP addresses that you want to release.


## Next steps

[Add a network virtualization gateway to the VMM fabric](network-gateway.md).
