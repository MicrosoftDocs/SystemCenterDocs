---
ms.assetid: 6c063660-b105-4f68-915e-3adc9021a14a
title: Manage the SDN infrastructure in the VMM fabric
description: This article describes how manage SDN networking elements in the System Center VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  01/24/2017
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Manage SDN resources in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

 This article summarizes the software-defined network (SDN) operations that you can manage in the VMM fabric. For operations that can't be managed in the fabric, you need to use REST APIs or Windows Server PowerShell.

 A software-defined network (SDN) abstract physical hardware network infrastructure into virtual networks. In the VMM fabric you can deploy and manage an SDN infrastructure, including network controller, software load balancers, and gateways, to provision and manage virtual networks at scale. Learn more(../scenario/sdn-overview.md).


## What can I manage in VMM?

SDN resources fall into two broad categories in VMM:

- **Known resources**: Resources that can be created and managed with VMM
- **Unknow resources**: Resources that must be created and managed outside of VMM.


### Known resources

These resources can be created and managed with or without VMM. If you make changes to these resources outside VMM, VMM overwrites the out-of-box changes, when a VMM operation is performed on the object. This could cause configuration and connectivity issues, and should be avoided whenever possible. There's no way to revert an overwrite unless you detect the issue, and reconfigure manually.

We strongly recommend that you configure resources that are known to VMM in the VMM fabric only.

**Known object** | **Details**
--- | ---
AccessControlList | An AccessControlList contains a list of ACL rules, and can be assigned to virtual subnets or IP configurations. | Overwritten by VMM if you enable out-of-box
AclRule | Summarizes the network traffic that is allowed or denied for a VM network interface. | Overwritten by VMM if you enable out-of-box
Gateway | Provides gateway services to one or more virtualNetworks. | Overwritten by VMM if you enable out-of-box
GatewayPool | GatewayPools aggregate a set of gateways resources into a single pool.  | Overwritten by VMM if you enable out-of-box
Host | | Overwritten by VMM if you enable out-of-box
HostProperties | | Overwritten by VMM if you enable out-of-box
IpConfigurations | IP addresses of the load balancer | Overwritten by VMM if you enable out-of-box
IpPool | Create an IP address pool on the network controller | Overwritten by VMM if you enable out-of-box
LoadBalancerManager | Configures the load balancing service of the Network Controller. | Overwritten by VMM if you enable out-of-box
LoadBalancerMux |  Represents a MUX VM deployed in the network controller fabric. | Overwritten by VMM if you enable out-of-box
LogicalSubnets | A subnet/VLAN pair. | Overwritten by VMM if you enable out-of-box
MACPool | Creates a MAC address pool on the network controller | Overwritten by VMM if you enable out-of-box
NatRules | Configures the load balancer to apply NAT to traffic | Overwritten by VMM if you enable out-of-box
NetworkInterface |Specifies the configuration of either a host virtual interface (host vNIC) or a virtual server NIC (VMNIC).  | Overwritten by VMM if you enable out-of-box
PortSettings | Overwritten by VMM if you enable out-of-box
PublicIPAddress | Specifies an IP address which is publically available. It's used by virtualGateways and loadBalancers to indicate the IP address that can be used to communicate with the virtual network from outside. | Overwritten by VMM if you enable out-of-box
QualityOfService | | Overwritten by VMM if you enable out-of-box
Servers | Represents a physical server that is being controlled by the Network Controller. | Overwritten by VMM if you enable out-of-box
VirtualGateway | Describes the gateway used for cross-premises connectivity from the virtual network. | Overwritten by VMM if you enable out-of-box
VirtualGatewayBgpPeer | Configures BGP peers of the virtualGateways resource. | Overwritten by VMM if you enable out-of-box
VirtualNetwork | Used to create a virtual network using HNV for tenant overlays.  | Overwritten by VMM if you enable out-of-box
VirtualServer | Corresponds to a virtual machine. Must be created for VMs that correspond to gateway and MUX resources. | Overwritten by VMM if you enable out-of-box
VirtualSubnet | Used to create virtual subnets (VSIDs) under a tenant's virtual network (RDID). | Overwritten by VMM if you enable out-of-box
VirtualSwitchManager | Configures the virtual switch properties on every server managed by the Network Controller | Overwritten by VMM if you enable out-of-box
VM | Corresponds to a virtual machine. | Overwritten by VMM if you enable out-of-box



### Unknown resources

These resources to be created and managed outside the VMM fabric. VMM has no knowledge of them, and obviously doesn't overwrite them when they're configured outside the VMM console.

Unknown objects are any Network Controller resources that aren't listed in the table above. Get the [latest list](https://msdn.microsoft.com/en-us/library/mt758684.aspx) of SDN resources.
