---
ms.assetid: ea90aa0a-46e0-49f0-8560-5c35dd3a3c96
title: Fabric Monitoring in System Center Operation Manager
description: This article provides an overview of fabric monitoring.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Fabric Monitoring



A close integration between System Center Virtual Machine Manager and System Center Operations Manager introduces System Center cloud monitoring of virtual layers for private cloud environments. The management pack for System Center Virtual Machine Manager monitors availability of VMM and the availability, health, and performance of all virtual machines and virtual machine hosts that VMM manages. The Fabric Health Dashboard shows a detailed overview of the health of your private clouds and the fabric that services those clouds. The dashboard helps you answer questions like "What is the health of my clouds and the fabric serving those clouds?" and helps you understand how your fabric components are connected. At a glance, you can see cloud health and the health of the underlying fabric/virtual machines. You can also do the root cause analysis by linking to existing dashboards, such as network monitoring dashboards, and the Virtual Machine Manager diagram view can help you dive into network and storage monitoring.

To get the dashboard, use the System Center management pack for System Center Virtual Machine Manager Fabric Health Dashboard, which is imported automatically when you integrate Operations Manager and Virtual Machine Manager.

## Fabric of a private cloud

The fabric of a private cloud consists of physical and virtual elements that fall into three main categories: Compute, Storage, and Hardware.

- **Compute**  includes hosts, operating systems/platforms that are running on the hosts, workloads (what's running on your private cloud, such as SQL, AD, DNS, DHCP), workload configuration, and management infrastructure.
- **Storage**  includes file shares, LUNs, and storage pools.
- **Hardware**  includes physical and virtual network devices and networks, as well as fabric hardware.

## Before you begin

Virtual Machine Manager controls the private cloud. Before you can begin to monitor the fabric of your private clouds, you must integrate System Center Operations Manager and Virtual Machine Manager. For details, see [Configuring Operations Manager integration with VMM](plan-thirdparty-integration.md). During the integration, several management packs are imported automatically, including the Management Pack for System Center Virtual Machine Manager and the Management Pack for Virtual Machine Manager Fabric Health Dashboard.

The Management Pack for System Center Virtual Machine Manager monitors availability of VMM and the availability, health, and performance of all virtual machines and virtual machine hosts that VMM manages. You must install this management pack before you can configure the following VMM features: Performance and Resource Optimization (PRO), Maintenance Mode integration, Reporting in VMM, and Support for SQL Server Analysis Services (SSAS).

The VMM management pack enables the integration of Operations Manager with VMM and monitors the health of virtual machines running on Microsoft Hyper-V, VMware ESX, and Citrix XenServer. For more information, see [Operations Manager monitoring scenarios](manage-monitoring-scenarios.md).

The VMM Fabric Health Dashboard management pack displays much of what the VMM management pack monitors into a dashboard view.

## Next steps

- [Scoping the Fabric Health Dashboard to a specific cloud](scope-fabric-health-dashboard.md)
- [Fabric Monitoring diagram view](fabric-monitoring-diagram-view.md)
- [Monitor cloud fabric using System Center Advisor](use-system-center-advisor.md)
