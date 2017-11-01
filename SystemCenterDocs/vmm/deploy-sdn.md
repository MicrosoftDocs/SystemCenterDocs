---
ms.assetid: dbb10ddd-b976-4cb6-9216-ec70eafca4b6
title: Deploy and manage a Software Defined Network (SDN) infrastructure in System Center VMM
description: This article provides an overview of setting up n SDN in the System Center VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Deploy and manage a Software Defined Network (SDN) infrastructure in the VMM fabric

>Applies To: System Center 2016- Virtual Machine Manager

System Center - Virtual Machine Manager (VMM) can be used to deploy and manage a Software Defined Network (SDN) infrastructure.

## Software Defined Network overview
SDN virtualizes your network to abstract physical hardware network elements such as switches and routers. Using SDN you can dynamically manage your datacenter networking to meet workload and app requirements. Network policies can be implemented consistently, at scale, even as you deploy new workloads, or move workloads across virtual or physical networks.

If you deploy SDN in the VMM fabric you can:

- Provision and manage virtual networks at scale.
- Deploy and manage the SDN infrastructure, including network controllers, software load balancers, and gateways.
- Define and control virtual network policies centrally and link them to your applications or workloads. When your workload is deployed or moved, the network configuration adjusts itself automatically. This is important because it removes the need for manual reconfiguration of network hardware, thereby reducing operational complexity while saving your valuable resources for higher-impact work.
- Control traffic flow between virtual networks, including the ability to define guaranteed bandwidth for your critical applications and workloads.

SDN combines a number of technologies, among them:

- **Network Controller**:The network controller allows you to automate configuration of your network infrastructure, instead of manually configuring network devices and services.
- **RAS Gateway for SDN**: RAS Gateway is a software-based, multitenant, BGP capable router in Windows Server 2016 that is designed for CSPs and Enterprises that host multiple tenant virtual networks using HNV.
- **Software Load Balancing (SLB) for SDN**: (SDN) in Windows Server 2016 can use Software Load Balancing (SLB) to evenly distribute tenant and tenant customer network traffic among virtual network resources. The Windows Server SLB enables multiple servers to host the same workload, providing high availability and scalability.

[Read more about](https://technet.microsoft.com/library/mt590952.aspx) technologies in the SDN stack.


## Next steps

- [Deploy SDN components using PowerShell](sdn-powershell.md)
- Alternatively, deploy SDN components manually in the VMM console:
    - [Set up a network controller](sdn-controller.md)
    - [Set up a software load balancer](sdn-slb.md)
    - [Set up a RAS gateway](sdn-gateway.md)
