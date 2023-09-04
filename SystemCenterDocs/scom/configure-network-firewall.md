---
ms.assetid: 
title: Configure the network firewall
description: This article describes how to configure the network firewall.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 09/01/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Configure the network firewall

This article describes how to configure the network firewall and Azure NSG rules.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Network prerequisites

### Establish direct connectivity (line of sight) between your domain controller and the Azure network

Ensure that there's direct network connectivity (line of sight) between the network that has your desired domain controller and the Azure subnet (VNet) in which you deploy a SCOM Managed Instance. Ensure that there's direct network connectivity (line of sight) between the workloads/agents and the Azure subnet in which SCOM Managed Instance is deployed.

This is required so that all your following resources can communicate with each other over the network:
- Domain controller
- Agents
- System Center Operations Manager components such as the Ops console
- SCOM Managed Instance (preview) components such as management servers

Following are the three distinct network models visually represented to create the SCOM Managed Instance.

#### Network Model 1 - The domain controller is located on-premises

In this model, the desired domain controller is located within your on-premises network. You must establish an Express Route connection between your on-premises network and the Azure subnet used for the SCOM Managed Instance.

If your domain controller and other component are in on-premises, you must establish the line of sight through Azure ExpressRoute or VPN. For more information, see [ExpressRoute documentation](/azure/expressroute/) and [Azure VPN Gateway documentation](/azure/vpn-gateway/).

Following is the network model, wherein the desired domain controller is situated within the on-premises network. There exists a direct connection (via Express Route or VPN) between the on-premises network and the Azure subnet used for SCOM Managed Instance creation.

:::image type="Network model 1" source="media/configure-network-firewall/network-model-1-inline.png" alt-text="Screenshot describing the network model 1 - domain controller is located on-premises." lightbox="media/configure-network-firewall/network-model-1-expanded.png":::

#### Network model 2 - The domain controller is hosted in Azure

In this configuration, the designated domain controller is hosted in Microsoft Azure, and you must establish an Express Route or VPN connection between your on-premises network and the Azure subnet. This is used for the SCOM Managed Instance creation and to Azure subnet used for the designated domain controller. For more information, see [ExpressRoute](/azure/expressroute/) and [Azure VPN Gateway](/azure/vpn-gateway/).

In this model, the desired domain controller remains integrated into your on-premises domain forest. However, you chose to create a dedicated Active Directory controller in Microsoft Azure to support Azure resources that rely on the on-premises Active Directory infrastructure.

:::image type="Network model 2" source="media/configure-network-firewall/network-model-2-inline.png" alt-text="Screenshot describing network model 2 - domain controller is hosted in Azure." lightbox="media/configure-network-firewall/network-model-2-expanded.png":::

### Network model 3 - The domain controller and SCOM managed instances are in Azure VNets

In this model, both the desired domain controller and the SCOM Managed Instances are placed in separate and dedicated Virtual Networks (VNets) in Azure.

If your desired domain controller and all other components are in same virtual network of Azure (a conventional active domain controller) with no presence in on-premises, then you'll already have a line of sight between all your components.

If your desired domain controller and all other components are in different virtual networks of Azure (a conventional active domain controller) with no presence on-premises, then you need to do virtual network peering between all the virtual networks that are in your network. For more information, see  [Virtual network peering in Azure](/azure/virtual-network/virtual-network-peering-overview).

:::image type="Network model 3" source="media/configure-network-firewall/network-model-3-inline.png" alt-text="Screenshot describing network model 3 - domain controller and SCOM managed instances are in Azure VNets." lightbox="media/configure-network-firewall/network-model-3-expanded.png":::

Ensure to take care of the following for all the three networking models mentioned earlier:

1. Ensure that the SCOM Managed Instance subnet can establish connectivity to the designated domain controller configured for Azure or SCOM Managed Instance. Also, ensure that domain name resolution within the SCOM Managed Instance subnet lists the designated domain controller as the top entry among the resolved domain controllers to avoid network latency/performance and firewall issues.

2. The following ports on the designated domain controller and DNS must be accessible from the SCOM Managed Instance subnet:
     - TCP port 389 or 636 for LDAP
     - TCP port 3268 or 3269 for global catalog
     - TCP and UDP port 88 for Kerberos
     - TCP and UDP port 53 for DNS
     - TCP 9389 for Active directory webservice
     - TCP 445 for SMB
     - TCP 135 for RPC

       The internal firewall rules and network security group (NSG) must allow communication from SCOM Managed Instance virtual network and the designated domain controller/DNS for all the ports listed earlier.

3. The SQL MI VNet and SCOM Managed Instance must be peered to establish connectivity. Specifically, the port 1433(private port) or 3342(public port) must be reachable from the SCOM Managed Instance to the SQL MI. Configure the NSG rules and firewall rules on both virtual networks to allow ports 1433 and 3342.

4. Allow communication on ports 5723, 5724, and 443 between SCOM Managed Instance (preview) and the machine being monitored, and vice versa.

      - If the machine is on-premises, set up the NSG rules and firewall rules on the SCOM Managed Instance subnet and on the on-premises network where the monitored machine is located to ensure specified essential ports (5723, 5724, and 443) are reachable from monitored machine to SCOM Managed Instance subnet.
      
      - If the machine is in Azure, set up the NSG rules and firewall rules on the SCOM Managed Instance's VNet and on the virtual network where the monitored machine is located to ensure specified essential ports (5723, 5724, and 443) are reachable from monitored machine to SCOM Managed Instance subnet.

5. Enable NAT gateway on the SCOM Managed Instance subnet to download the System Center Operations Manager installer from Azure storage account and install.

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](scom-managed-instance-self-verification-of-steps.md). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions from Operations Manager admin to AD Admin and network admin. This saves time of AD admin, Network admin and System Center Operations Manager admin.

## Next steps

- [Verify Azure and internal GPO policies](verify-azure-and-internal-gpo-policies.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
