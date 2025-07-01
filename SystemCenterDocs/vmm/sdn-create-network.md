---
ms.assetid: 2e2323c5-6ec6-4fd2-bec5-70537d328fbe
title: Set up a Virtual Network in SDN in the VMM Fabric
description: This article describes the procedure on how to create a VM network in SDN, using a VMM.
author: jyothisuri
ms.author: jsuri
ms.date: 04/08/2025
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---


# Set up VM networks in SDN using VMM



This article provides information about how to create VM networks in an SDN using System Center Virtual Machine Manager (VMM).

VM networks are abstract objects that act as an interface to logical networks. In a virtualized network environment, by using the VM networks, you can abstract virtual machines from the underlying logical network.

::: moniker range=">=sc-vmm-2022"

VMM 2025 and 2022 provide dual stack support for VM networks.

::: moniker-end

A logical network can have one or more VM networks associated with it based on its isolation settings.

The following two types of isolation settings are supported in SDN fabric:

- **Network virtualization**: If a logical network is isolated using network virtualization, you can create multiple VM networks for this logical network. Within a VM network, tenants can use any IP addresses regardless of the IP addresses used on other VM networks. As a service provider, you can host workloads from multiple tenants on a single logical network. Tenants can also configure network connections on these VM networks.

- **No Isolation**:  If a logical network has no isolation, then only a single VM network can be associated with it. As a service provider, you can host infrastructure workloads using this type of isolation settings.

>[!NOTE]
> VLAN isolation is not supported in SDN fabric.

## Before you start

 Here are some considerations before you set up VM networks in SDN using VMM:

- Network controller is deployed in the SDN fabric. [Learn more](sdn-controller.md).

- A logical network with appropriate isolation settings is created and is set to be managed by the Microsoft network controller. Also, create the IP pools for this logical network.

>[!NOTE]  
> If you want to deploy the VMs with dynamic IP on **no isolation** network, then IP pools are not required.

- By default, VMs connected to a VM network with network virtualization isolation setting can't connect to other networks. If you want your VM network to connect to other networks, you need to first deploy [SDN SLB ](sdn-slb.md) and [SDN gateway](sdn-gateway.md).

::: moniker range="<=sc-vmm-2019"

## Create a VM network (network virtualization)

To create a VM network, follow these steps:

1. In the VMM fabric, select **VMs and Services** > **VM Networks** > **Create VM Network**.
2. In **Create VM Network Wizard** > **Name**, enter a name and optional description, and select a logical network that was created with network virtualization isolation settings.
3. In **Isolation**, select **Isolate using Hyper-V network virtualization**, and then select IPv4 for IP address protocols for the VM network. Select **Next**.

   ![Screenshot of VM network in sdn.](media/sdn-create-network/vm-network.png)

4. In **VM Subnets**, select **Add**, specify the name and subnets for VM network, and then select **Next**.

   >[!NOTE]  
   > You can add multiple subnets.

5. In **Connectivity** panel, select the type of connectivity you want to use for this VM network.

   >[!NOTE]
   > By default, all virtual machines in a VM network communicate with each other. If you want virtual machines on this VM network to communicate with other networks, configure the following settings in the **Connectivity** page:



   - **Connect to another network through a VPN tunnel**: Select this option if you want the virtual machines on this VM network to communicate with other networks over a VPN. To automatically learn routes between the sites connected through the VPN tunnel, select the **Enable the border gateway protocol** option.  Select the **VPN gateway device** that you want to use and confirm the settings.

     Based on your selection, the **VPN Connections** and **Border Gateway Protocol** pages appear. Complete the settings based on the information provided by the VPN admin.

   - **Connect directly to an additional logical network**: Select this option if you want the virtual machines on this VM network to connect directly to an additional logical network. To enable access to internet resources, select **Network Address Translation (NAT)** or select **Direct Routing** to bridge a virtualized IP address space with a physical IP address space.

6. In **Summary**, verify the settings and select **Finish**.

Once the job is successfully completed, you can view the newly created VM network under **VMs and Services** > **VM Networks**.

> [!NOTE]
> After you create a VM network with network virtualization, ensure that you [create an IP Pool](network-pool.md#set-up-an-ip-address-pool-on-a-vm-network) for this VM network.


::: moniker-end

::: moniker range="sc-vmm-2022"

## Create a VM network (network virtualization)

To create a VM network, follow these steps:

1. In the VMM fabric, select **VMs and Services** > **VM Networks** > **Create VM Network**.
2. In **Create VM Network Wizard** > **Name**, enter a name and optional description, and select a logical network that was created with network virtualization isolation settings.
3. In **Isolation**, select **Isolate using Hyper-V network virtualization**, and then select IPv4 for IP address protocols for the VM network. Select **Next**.
4. To enable dual stack support in Isolation, select **Isolate using Hyper-V network virtualization**, and then select **IPv4 and IPv6** for **IP address protocols for the VM network**. Select **Next**.

   ![VM network in sdn](media/sdn-create-network/vm-network.png)

5. In **VM Subnets**, select **Add**, specify the name and subnets for VM network, and then select **Next**.

   >[!NOTE]
   >- You can add multiple subnets.
   >- To enable dual stack support, provide both IPv4 subnet and IPv6 subnet separated by a semicolon (;).
   >- For VM network with dual stack support, create two static IP pools with both IPv4 and IPv6 address space.

6. In **Connectivity** panel, select the type of connectivity you want to use for this VM network.

   >[!NOTE]
   > By default, all virtual machines in a VM network communicate with each other. If you want virtual machines on this VM network to communicate with other networks, configure the following settings in the **Connectivity** page:



   - **Connect to another network through a VPN tunnel**: Select this option if you want the virtual machines on this VM network to communicate with other networks over a VPN. To automatically learn routes between the sites connected through the VPN tunnel, select the **Enable the border gateway protocol** option. Select the **VPN gateway device** that you want to use and confirm the settings.

     Based on your selection, the **VPN Connections** and **Border Gateway Protocol** pages appear. Complete the settings based on the information provided by the VPN admin.

   - **Connect directly to an additional logical network**: Select this option if you want the virtual machines on this VM network to connect directly to an additional logical network. To enable access to internet resources, select **Network Address Translation (NAT)** or select **Direct Routing** to bridge a virtualized IP address space with a physical IP address space.

7. In **Summary**, verify the settings and select **Finish**.

Once the job is completed successfully, you can view the newly created VM network under **VMs and Services** > **VM Networks**.

> [!NOTE]
> After you create a VM network with network virtualization, ensure that you [create an IP Pool](network-pool.md#set-up-an-ip-address-pool-on-a-vm-network) for this VM network.

::: moniker-end

## Create a VM network (no isolation)

> [!NOTE]
> While creating the logical network, if you have chosen the option **Create VM network with same name to allow virtual machines to access this logical network directly**, then you can skip the following steps.

To create a VM network, follow these steps:

1. Select **VMs and Services** > **VM Networks** . **Create VM Network**.
2. In **Create VM Network Wizard** > **Name**, enter a name and optional description. Select a **One connected logical network** for this VM network. Select **Next**.
3. In **Summary**, verify the settings and select **Finish**.

Once the job is successfully completed, you can view the newly created VM network under **VMs and Services** > **VM Networks**.

> [!NOTE]
>If you had created an IP pool on the logical network, the same will be directly available for the VM network.

## Next steps

[Create an IP pool for a VM network](network-pool.md#set-up-an-ip-address-pool-on-a-vm-network).
