---
ms.assetid: d174e976-e265-4acc-9ef5-1c92b602f761
title: Set up NAT for traffic forwarding in SDN infrastructure by using VMM.
description: This article describes how to configure NAT connection and NAT rules for traffic forwarding in the SDN infrastructure.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Set up NAT for traffic forwarding in the SDN infrastructure



This article describes how to set up Network Address Translation (NAT) for traffic forwarding in a software-defined network (SDN) infrastructure set up in the System Center Virtual Machine Manager (VMM) fabric.

NAT allows virtual machines (VMs) in an isolated SDN virtual network to obtain external connectivity. VMM configures a Virtual IP (VIP) to forward the traffic to and from an external network.

The following two NAT types are supported by VMM.

- **Outbound NAT** - Forwards the VM network traffic from a virtual network to external destinations.
- **Inbound NAT** - Forwards the external traffic to a specific VM in a virtual network.

This article provides information about how to configure a NAT connection for SDN virtual networks using VMM.

::: moniker range=">=sc-vmm-2022"

VMM 2025 and 2022 support dual stack. NAT rules to Dual stack VM networks isn't supported at VMM console. NAT rules can be specified using PowerShell cmdlets. For more information, see [Add rules to a NAT connection](#add-rules-to-a-nat-connection).

::: moniker-end

::: moniker range="sc-vmm-2019"

>[!NOTE]
>- From VMM 2019 UR1, **One Connected** network type is changed to **Connected Network**
>- VMM 2019 UR2 and later supports IPv6.

::: moniker-end

## Before you start

Ensure the following:
- [SDN network controller](sdn-controller.md) and the SDN [software load balancer](sdn-slb.md) are deployed.
- An SDN VM network with network virtualization is created.

## Create a NAT connection

Use the following procedure:

1. In the VMM console, select **VMs and Services** > **VM Networks**. Right-click the selected VM network for which you want to create the NAT connection and select **Properties**.
2. Select **Connectivity** on the wizard page displayed.

3. In **Connectivity**, select **Connect directly to an additional logical network** and select **Network address translation (NAT)** under this option.

    ![Screenshot of nat connection.](media/sdn-nat/create-connection-directly.png)

4. In the **IP address pool**, choose the IP pool from which the VIP must come from. In IP address, choose an IP address from the pool selected. Select **OK**.
::: moniker range=">=sc-vmm-2019"
5. To enable IPv6, select an IPv6 address pool and provide an IPv6 address.
::: moniker-end

A NAT connection will be created for this VM network.

> [!NOTE]
> - Along with the NAT connection, this procedure also creates  a default Outbound NAT rule that enables the outbound connectivity for the VM network.
> - To enable inbound connectivity and forward an external traffic to a specific VM, you must add NAT rules to the NAT connection.

## Add rules to a NAT connection

::: moniker range="<=sc-vmm-2019"
VMM 2022 supports dual stack. NAT rules to dual stack VM networks isn't supported at the VMM console. NAT rules can be specified using PowerShell cmdlets.
:::moniker-end

::: moniker range=">=sc-vmm-2022"
VMM 2025 and 2022 support dual stack. NAT rules to dual stack VM networks isn't supported at the VMM console. NAT rules can be specified using PowerShell cmdlets.
:::moniker-end

```
$vmNetwork = Get-SCVMNetwork -ID <VMNetwork ID>

$vmSubnet = Get-SCVMSubnet -Name <VMSubnet Name> | where { $_.ID -eq <VMSubnet ID> }
$gatewayDevice = Get-SCNetworkGateway -ID <Gateway Device ID>
$VmNetworkGateway = Add-SCVMNetworkGateway -Name "TenantDS_Gateway" -EnableBGP $false -NetworkGateway $gatewayDevice -VMNetwork $vmNetwork
```

**For IPv6 NAT Connection**

```
$externalIpPoolVar = Get-SCStaticIPAddressPool -ID <VIP Pool Id>
$natConnectionIPv6 = Add-SCNATConnection -VMNetwork $vmNetwork -Name "TenantDS_NatConnection_IPv6" -ExternalIPPool $externalIpPoolVar -ExternalIPAddress <IP From IPv6 VIP Pool>
Add-SCNATRule -Name "NATIPv6" -Protocol "TCP" -InternalIPAddress <IP From IPv6 subnet> -ExternalPort <External Port> -NATConnection $natConnectionIPv6 -InternalPort <Internal Port>
```

**For IPv4 NAT Connection**

```
$externalIpPoolVar1 = Get-SCStaticIPAddressPool -Name "PublicVIP_IPAddressPool_0"
$natConnectionIPv4 = Add-SCNATConnection -VMNetwork $vmNetwork -Name "TenantDS_NatConnection_IPv4" -ExternalIPPool $externalIpPoolVar1 -ExternalIPAddress <IP From IPv4 VIP Pool>
Add-SCNATRule -Name "NATIPv4" -Protocol "TCP" -InternalIPAddress <IP From IPv4 subnet>" -ExternalPort <External Port> -NATConnection $natConnectionIPv4 -InternalPort <Internal Port>
```

Use the following procedure to add rules to a NAT connection:

1.	In the VMM console, select **VMs and Services** > **VM Networks**. Right-click the selected VM network and select **Properties**.
2.	Select **Network Address Translation** on the wizard.

    ![Screenshot of nat rules.](media/sdn-nat/nat-rules.png)
3.	Under **Specify network address translation (NAT) rules**, select **Add**.
Type the following details as appropriate:

   - **Name** – Name for the inbound NAT rule.
   - **Protocol** – Inbound network traffic protocol. TCP/UDP are supported.
   - **Incoming Port** – Port number that you want to use along with the VIP to access the VM.
   - **Destination IP** – IP address of the VM to which you want to direct the external traffic.
   - **Destination Port** – Port number on the VM, the external traffic must be forwarded to.
4.	Select **OK**.

>[!NOTE]
> Multiple NAT rules can be created to forward the traffic to multiple VMs that are part of the VM network.

## Remove a NAT rule
Use the following procedure:

1. In the VMM console, select **VMs and Services** > **VM Networks**. Right-click the selected VM network and select **Properties**.
2. Select **Network Address Translation** on the wizard.
3. Select the NAT rule that you want to remove, select **Remove**, and then select **OK**.

## Remove a NAT connection
1.	In the VMM console, select **VMs and Services** > **VM Networks**. Right-click the selected VM network and select **Properties**.
2. Select **Connectivity** on the wizard.
3. Clear the option **Connect directly to an additional logical network** and select **OK**.
