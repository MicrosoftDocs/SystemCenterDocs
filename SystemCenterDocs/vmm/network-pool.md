---
ms.assetid: a0d8b08f-b44f-476e-a530-493378c2e4da
title: Set up static IP address pools in the VMM fabric
description: This article describes how to set up IP address pools in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Set up static IP address pools in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to set up static IP address pools for logical and VM networks in the System Center - Virtual Machine Manager (VMM) networking fabric.

When you set up the logical network you'll need to configure a static IP address pool if you're not using DHCP. In some circumstances you'll need to create IP address pools on the logical network only, and in others you'll need to create the pool on both the logical and VM networks:

- **Pool on logical and VM network**: If you configure your logical network for network virtualization you'll need to create IP address pools on the logical network and the VM network.
- **Pool on logical network only**: If you're using VLAN or no isolation you can use DHCP or create IP address pools on the logical network only. They'll automatically become available on the VM network.
- **Imported address pools**: If you are using external networks through a vendor console your IP address pools will be imported from the vendor and you don't need to create them in VMM.


## Create a static address pool for a logical network

1. in **Logical Networks and IP Pools** click the logical network > **Home** > **Create** > **Create IP Pool**.
2. In **Create Static IP Address Pool Wizard** > **Name** specify a name and description. Make sure the correct logical network is indicated.
3. In **Network Site** select to use an existing site and select the IP subnet, or create a new site.

	- For an existing site select the site and IP subnet from which to create the pool.
	- For a new stie specify the site name, IP subnet to assign to the site, and VLAN information if relevant. Select the host groups that can access this site and the logical network.
4. If you're using network virtualization you can use the pool to support multicasting or broadcasting. To do this click **Create a multicast IP address pool** and select the IP subnet you want to use. To use multicasting or broadcasting note that:

	- The logical network must have network virtualization enabled.
	- The IP protocol setting for the VM network must match the IP protocol settings for the underlying logical network. You can't view the protocol setting in the VMM console after you've created it. You'll need to run **Get-SCVMMNEtwork -Name <VM network name> | Format -List Name, Isolation Type, PoolType** to see it.
	- After you've configured this feature multicast and broadcast packets on the VM network will use the IP addresses from the multicast IP address pool. Each subnet in the VM network will consume one IP address from the multicast pool.

5. In **IP address range** enter the start and end address for the pool. They must be contained within the subnet. In **VIPs and reserved IP addresses** specify IP address range you want to reserve for VIPs. VIPS are used during deployment of a service in a load-balanced service tier. VMM automatically assigns a VIP to the load balancer from the reserved VIP address range.
6. In **Gateway** click **Insert** if you want to specify one or more default gateways and the metric. The default gateway address must be in the same subnet range as the IP address pool but doesn't need to be part of the pool.
7. In **DNS** specify DNS information, including DNS servers, the default DNS suffix for the connection, and the list of DNS search suffixes.
8. In **WINS** click **Insert** if you want to enter the IP address of a WINS server. You can also select whether to enable NetBIOS over TCP/IP. This isn't recommended if the address range is made up of public addresses.
9. In **Summary** verify the settings and click **Finish**. When the job shows as **Completed** verify the pool in **Logical Networks and IP Pools**.

## Set up an IP address pool on a VM network

1. Click **VMs and Services** > **VM Networks**  > **Home** > **Show** > **VM Networks** > **VM Network** tab.
2. In  **VM Networks and IP Pools** click the VM network **Create** > **Create IP Pool**.
2. In **Create Static IP Address Pool Wizard** > **Name** specify a name and description. Make sure the correct logical network is indicated. Check that the correct VM network and subnet is selected.
3. In **IP address range** enter the start and end address for the pool. You can create multiple IP address pools in a subnet but the ranges mustn't overlap. In **Reserved IP addresses** specify any ranges you want to reserve for other purposes.
6. In **Gateway** click **Insert** if you want to specify one or more default gateways and the metric. The default gateway address must be in the same subnet range as the IP address pool but doesn't need to be part of the pool.
7. In **DNS** specify DNS information, including DNS servers, the default DNS suffix for the connection, and the list of DNS search suffixes. For virtual machines that will join an Active Directory domain, we recommend that you use Group Policy to set the primary DNS suffix. This will ensure that when a Windows-based virtual machine is set to register its IP addresses with the primary DNS suffix, a Windows-based DNS server will register the IP address dynamically. Additionally, the use of Group Policy enables you to have an IP address pool that spans multiple domains. In this case, you would not want to specify a single primary DNS suffix.
8. In **WINS** click **Insert** if you want to enter the IP address of a WINS server. You can also select whether to enable NetBIOS over TCP/IP. This isn't recommended if the address range is made up of public addresses.
9. In **Summary** verify the settings and click **Finish**. When the job shows as **Completed** verify the pool in **Logical Networks and IP Pools**.


### Release inactive addresses from the static address pool

You can release inactive addresses. When you do VMM returns the address to the static IP or MAC address pool and considers it available for reassignment. An address is considered inactive if:

- A host that was assigned a static IP address through the bare-metal deployment process is removed from VMM management. When you remove the host, any IP and MAC addresses that were statically assigned to virtual machines on the host are also marked as inactive.
- A virtual machine goes into a missing state because it was removed outside VMM.

1. Release  the IP addresses:

	- To release addresses in a pool in a logical network click **Logical Networks and IP Pools** expand the logical network and click the IP address pool.
	- To release addresses in a pool in a VM network click **Logical Networks and IP Pools** expand the VM network and click the IP address pool.
2. Click **Home** > **Properties** > **Inactive addresses** and select the inactive IP addresses that you want to release.


## Next steps

[Create a VM network](network-virtual.md)
