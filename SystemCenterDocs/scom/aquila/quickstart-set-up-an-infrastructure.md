---
ms.assetid: 
title: Set up an infrastructure
description: This quickstart describes how to set up your existing infrastructure before deploying Aquila. 
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.date: 10/06/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Quick Start: Set up an infrastructure

This quickstart describes how to set up your existing infrastructure before deploying Aquila. 

## Establish direct connectivity (line-of-sight) between your DC and your Azure network

- Ensure that there is direct network connectivity (line-of-sight) between the network, which has your Domain Controller, Ops Console, Agents, and the network in which you will deploy an Aquila instance. This is required so that all your resources (Domain Controller, System Center Operations Manager Components such as Ops Console, Aquila Components such as Management Servers) can talk to each other over the network.
- If your Domain Controller or any other component is on-premises, the line-of-sight can be established through *ExpressRoute* or *VPN*. For more information, see [ExpressRoute](/azure/expressroute/) and [VPN Gateway](/azure/vpn-gateway/)
- If your Domain Controller and all other components are in Azure with no presence on-premises, a VPN network will work (ExpressRoute is not needed). If you are using one VPN to host all your components, you will already have a line-of-sight between all your components. If you have multiple VPNs, you will need to do VPN peering between all the VPNs that are in your network
- Allow Port 5723/5724/443 to communicate while talking from Aquila to the VMs being monitored and vice versa.

## Configure one domain account in Active Directory

- Create one domain account in your Active Directory. The domain account is a typical Active Directory account (it can be a non-admin account). This account will be used to join the Management Servers (that will, in the future, be automatically created by Aquila) to your existing domain.
- Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain.
- You can use an existing domain account if it has these [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain).

## Next steps

> [!div class="nextstepaction"]
> [Set up Microsoft Azure for Managed service identity, Aquila RBAC and SQL MI instance](quickstart-azure-for-managed-service-identity-aquila-sql-mi-instance.md)