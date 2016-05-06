---
title: Fabric Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 532a7c83-4304-4ab7-839b-6d1fb1aa04f0
---
# Fabric Monitoring
A close integration between [!INCLUDE[vmmblue_1](../Token/vmmblue_1_md.md)] and [!INCLUDE[omblue_1](../Token/omblue_1_md.md)] introduces System Center cloud monitoring of virtual layers for private cloud environments. The Management Pack for System Center 2012 \- Virtual Machine Manager monitors availability of VMM and the availability, health, and performance of all virtual machines and virtual machine hosts that VMM manages. The Fabric Health Dashboard shows a detailed overview of the health of your private clouds and the fabric that services those clouds. The dashboard helps you answer questions like “What is the health of my clouds and the fabric serving those clouds?” and helps you understand how your fabric components are connected. At a glance, you can see cloud health and the health of the underlying fabric\/virtual machines. You can also do root cause analysis by linking to existing dashboards, such as network monitoring dashboards and the [!INCLUDE[vmmblue_2](../Token/vmmblue_2_md.md)] diagram view can help you dive into network and storage monitoring.

To get the dashboard, use the System Center 2012 Management Pack for [!INCLUDE[vmmblue_1](../Token/vmmblue_1_md.md)] Fabric Health Dashboard, which is imported automatically when you integrate [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] and Virtual Machine Manager.

## What is the Fabric of a Private Cloud?
The fabric of a private cloud consists of physical and virtual elements that fall into three main categories: Compute, Storage, and Hardware.

-   **Compute** includes hosts, operating systems\/platforms that are running on the hosts, workloads \(what’s running on your private cloud, such as SQL, AD, DNS, DHCP\), workload configuration, and management infrastructure.

-   **Storage** includes file shares, LUNs, storage pools.

-   **Hardware** includes physical and virtual network devices and networks, as well as fabric hardware.

## Before You Begin
Virtual Machine Manager controls the private cloud. Before you can begin to monitor the fabric of your private clouds, you must integrate [!INCLUDE[omblue_1](../Token/omblue_1_md.md)] and Virtual Machine Manager. For details, see [Configuring Operations Manager Integration with VMM](http://go.microsoft.com/fwlink/?LinkId=325587). During the integration, several management packs are imported automatically, including the Management Pack for System Center 2012 \- Virtual Machine Manager and the Management Pack for Virtual Machine Manager Fabric Health Dashboard.

The Management Pack for System Center 2012 \- Virtual Machine Manager monitors availability of VMM and the availability, health, and performance of all virtual machines and virtual machine hosts that VMM manages. You must install this management pack before you can configure the following VMM features: Performance and Resource Optimization \(PRO\), Maintenance Mode integration, Reporting in VMM, and Support for SQL Server Analysis Services \(SSAS\).

The VMM management pack enables the integration of Operations Manager with VMM and monitors the health of virtual machines running on Microsoft Hyper\-V, VMware ESX, and Citrix XenServer. In VMware vSphere 4 or VMware Infrastructure 3 \(VI3\) environments that are managed by using VMM, this management pack also monitors the health of virtual machines running on VMware ESX. For more information, see [Guide for System Center Monitoring Pack for System Center 2012 \- Virtual Machine Manager](http://technet.microsoft.com/library/jj126988.aspx).

The VMM Fabric Health Dashboard management pack displays much of what the VMM management pack monitors into a dashboard view.

## Fabric Monitoring Topics

-   [Getting Started with the Fabric Health Dashboard](../Topic/Getting-Started-with-the-Fabric-Health-Dashboard.md)

-   [Scoping the Fabric Health Dashboard to a Specific Cloud and Investigating Details](../Topic/Scoping-the-Fabric-Health-Dashboard-to-a-Specific-Cloud-and-Investigating-Details.md)

-   [The Fabric Monitoring Diagram View: Displaying Health States of Cloud Environments](../Topic/The-Fabric-Monitoring-Diagram-View--Displaying-Health-States-of-Cloud-Environments.md)

-   [Using System Center Advisor to Proactively Monitor Cloud Fabric](../Topic/Using-System-Center-Advisor-to-Proactively-Monitor-Cloud-Fabric.md)

-   [Monitoring a Private Cloud \- video series](https://curah.microsoft.com/217123/monitoring-a-private-cloud-video-series)

-   [How Healthy is Your Cloud? Fabric Monitoring Can Tell...](http://curah.microsoft.com/42340/how-healthy-is-your-cloud-fabric-monitoring-can-tell)

