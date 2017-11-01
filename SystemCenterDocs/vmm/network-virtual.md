---
ms.assetid: b48a7991-1138-4687-92e0-a9db8e6ae9b4
title: Set up VM networks in the VMM fabric
description: This article describes how to set up VM networks in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Set up VM networks in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to create VM networks based on System Center - Virtual Machine Manager (VMM) logical networks.


In a virtualized network environment, we want to abstract virtual machines from the underlying logical network. VM networks help you to do this. VM networks are abstract objects that act as an interface to logical networks.

- A logical network can have one or more associated VM networks.
- If a logical network isn't isolated, then a single VM network with be associated with it.
- If a logical network is isolated, then multiple VM networks can be associated with it. These multiple VM networks allow us to use networks for different purposes. For example, as a provider you might want to host workload for multiple tenants on a single logical network, using a separate VM network for each tenant. The type of VM network you set up depends on the isolation settings for the logical network:

    - **Network virtualization**: If the logical network is isolated using network virtualization you can create multiple VM networks for a logical network. Within a VM network tenants can use any IP addresses they want for their VMs regardless of the IP addresses used on other VM networks. Tenants can also configure some network settings.
    - **VLAN**: If the logical network is isolated using VLAN or PVLAN you'll create on VM network for each network site and VLAN in the logical network.
    - **No isolation**: If the logical network is configured without isolation you'll create a single VM network linked to a logical network.


## Before you start

- In some circumstances you'll need to create a static IP address pool on the VM network after you've created it. [Learn more](network-pool.md).
- By default machines within a specific VM network can connect to each other. If your VM network will connect to other networks you can configure it with a gateway (network service). If you want to add a gateway to the VM network you'll need to create it. [Learn more](network-gateway.md).


## Create a VM network (network virtualization)

1. Click **VMs and Services** > **VM Networks** > **Home** > **Create** > **Create VM Network**.
2. In **Create VM Network Wizard** > **Name**, type in a name and description and select a logical network on which to base the VM network.
3. In **Isolation**, select **Isolate using Hyper-V network virtualization**, and verify the IP address protocols.
4. In **VM Subnets** click **Add**, and specify subnets for the VM network using CIDR notation. You can add multiple subnets.
5. In **Connectivity**, if you see the message **No network service**, it specifies a gateway has been added to VMM and you can click **Next**. If you don't see the message, specify the gateway (network service) options:

    - **No connectivity**: Leave all check boxes cleared if the virtual machines on this VM network will communicate only with other virtual machines on this VM network. You can also leave clear if you plan to configure the gateway later.
    - **Connect to another network through a VPN tunnel**: Select this option if the virtual machines on this VM network will communicate with other networks over VPN. If the device will use the Border Gateway Protocol, enable this protocol. Select the VPN gateway device that you want to us. Confirm the settings. If the **VPN Connections** or Border Gateway Protocol pages appear, complete the settings based on information from the VPN admin.  page appears. If you selected the check box for Border Gateway Protocol, the Border Gateway Protocol page also appears.
    - **Connect directly to an additional logical network**: Select this option if the virtual machines on this VM network will communicate with other networks in this data center. Select either direct routing or NAT. Select the gateway device you want to use an confirm the settings.

6. In **Summary** verify settings and click **Finish**. Verify the network in **VM Networks and IP Pools**.



## Create a VM network (VLAN/PVLAN)

1. Click **VMs and Services** > **VM Networks** > **Home** > **Create** > **Create VM Network**.
2. In **Create VM Network Wizard** > **Name** type in a name and description and select a logical network on which to base the VM network.
3. In **Isolation Options**:

    - Select **Automatic** if you want VMM to automatically configure the isolation settings for the VM network. VMM will select a network site and subnet VLAN based on those available in the logical network.
    - Select **Specify a VLAN** to configure isolation manually. Note that tenant administrators can only select the **Automatic** option.
4. In **Summary** verify settings and click **Finish**. Verify the network in **VM Networks and IP Pools**.



## Create a VM network (no isolation)

1. Click **VMs and Services** > **VM Networks** > **Home** > **Create** > **Create VM Network**.
2. In **Create VM Network Wizard** > **Name** type in a name and description and select a logical network on which to base the VM network.
3. In **VM Networks and IP Pools** check for a VM network with the same name as the logical network you want to give direct access to. If one exists it probably indicates that the VM network was created automatically when you created the logical network. You can check whether the VM network provides direct access by clicking its properties. If **Name** and **Access** are the only tabs it provides direct access.
4. If there's no existing VM network click **Home** > **Create** > **Create VM Network**.
5. In **Summary** verify settings and click **Finish**. Verify the network in **VM Networks and IP Pools**.
