---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-08-23
title:  What's new in VMM in System Center Technical Preview
ms.technology:  virtual-machine-manager
ms.assetid:  2cfb6b1c-1694-4473-bd66-6c0fb91fe167
---

# What's new in VMM in System Center Technical Preview

This article describes what's new in Virtual Machine Manager (VMM) in System Center 2016 Technical Preview.


## Evaluation software for VMM in System Center 2016 Technical Preview

|Name|Description|Location|
|--------|---------------|------------|
|Evaluation VHD for VMM in System Center 2016 Technical Preview | Provides a downloadable pre-configured virtual hard disk (VHD) to create a virtual machine that runs an evaluation version of VMM in System Center 2016 Technical Preview.<br/><br/> Intended for evaluation and deployment planning purposes only.| [Microsoft Technet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-technical-preview)|

## Compute

### Full lifecycle management of Nano Server-based hosts and VMs

You can now use VMM to perform full lifecycle management of Nano Server-based hosts and virtual machines and leverage their benefits.

* **Prepare a Nano Server-based host for VMM management**: To get started with the lifecycle management of Nano Server you prepare a Nano Server-based host for VMM. [Learn more](../Manage/How-to-add-a-Nano-Server-as-a-Hyper-V-host-in-VMM.md).

* **Manage of Nano Server-based hosts and clusters (both compute and storage)**: You can now add and manage existing Nano Server-based standalone hosts, compute clusters, and storage clusters (both disaggregated and hyper-converged) using VMM. [Learn more](https://technet.microsoft.com/library/mt218831.aspx)

* **Bare metal deployment of Nano Server-based hosts and clusters (both compute and storage)**: You can now configure bare metal machines as Nano Server-based hosts, compute clusters, and storage clusters (both dis-aggregated and hyper-converged).  [Learn more](https://technet.microsoft.com/library/mt238025.aspx).


### Rolling Upgrade of a Windows Server 2012 R2 host cluster

You can now upgrade compute or storage clusters from Windows Server 2012 R2 to Windows Server 2016 Technical Preview with no downtime for the host workloads. VMM orchestrates the entire workflow of draining the node, evicting it, reinstalling the OS, and adding it back to the cluster. [Learn more](https://technet.microsoft.com/library/mt445417.aspx)

### Streamlined workflow for creating Hyper-V & SOFS clusters

With VMM 2016, creating Hyper-V host clusters and SOFS clusters is streamlined, as follows:

* **Bare metal deployment of Hyper-V host clusters**: We've simplified the workflow. Deploying a Hyper-V host cluster from bare metal machines is now a single step. [Learn more](https://technet.microsoft.com/library/mt238029.aspx)

* **Adding a bare-metal node to an existing Hyper-V host cluster or an SOFS Cluster**: You can now directly add a bare-metal computer to an existing Hyper-V or SOFS cluster. [Learn more](https://technet.microsoft.com/library/mt238035.aspx)

### New operations for running VMs

You can now increase/decrease static memory and add/remove virtual network adapter for a running VM. [Learn more](../Manage/Manage-Memory-for-a-VM-while-it-is-running.md) about managing static memory. [Learn more](../Manage/How-to-add-or-remove-a-vNIC.md) about removing a vNIC for a running VM.

### Production checkpoints

You can now create production checkpoints for VMs. These checkpoints are based on Volume Shadow Copy Service (VSS) and are application-consistent (compared to standard checkpoints based on Saved State technology that aren't application-consistent. [Learn more](../Manage/How-to-create-a-production-checkpoint-for-a-virtual-machine.md).

### Server App-V deprecation in VMM 2016

Server App-V application in service templates is deprecated in VMM 2016. You can no longer create a new template, or deploy a new service with the Server App-V package. If you upgrade from VMM 2012 R2 with a service with the Server App-V application, the existing service deployment will continue to work. This iensures that your existing service deployments aren't broken post upgrade. Post-upgrade you can't scale out the tier with Server App-V application. However scaling out of other tiers is possible.

## Storage

### Deploy and manage storage clusters with Storage Spaces Direct (S2D)

Windows Server 2016 Technical Preview introduces Storage Spaces Direct which enables you to build highly available storage systems that fit your specific needs, regardless of the exact configuration of your available storage systems. You can use VMM to create a Scale-Out File Server running Windows Server Technical Preview, and configure it with Storage Spaces Direct. Then you can create storage pools and file shares on the Scale-Out File Server.

-   Learn more about [deploying Storage Spaces Direct with VMM](../Manage/Deploying-Storage-Spaces-Direct-with-VMM.md)
-   Learn more about [Storage Spaces Direct in Windows Server Technical Preview](https://technet.microsoft.com/library/mt126109.aspx)

### Synchronously replicate storage volumes using Storage Replica (SR) 

With VMM 2016 you can protect data in a volume by synchronously replicating it between primary and secondary (recovery) volumes. You can deploy the primary and secondary volumes either to a single cluster, to two different clusters, or to two standalone servers. With VMM 2016 you can use PowerShell to setup Storage Replica between two volumes that are part of a single cluster. Once Storage Replica is setup you can use PowerShell to failover from the Primary Volume to the Recovery Volume.

-   Learn more about [deploying Storage Replica in VMM](../Manage/Deploying-Storage-Replica-in-VMM.md)
-   Read a [Storage Replica overview](https://technet.microsoft.com/library/mt126183.aspx)

### Configure Quality of Service (QoS) for storage

When hosts and storage are under heavy load, you might want to ensure that certain disks, virtual machines, applications, or tenants will not drop below a certain Quality of Service (QoS) for storage. VMM has been improved so it's easier to specify QoS. [Learn more](../Manage/Managing-storage-Quality-of-Service-policies-for-Scale-Out-File-Servers-in-VMM.md)


## Networking

### Template-based deployment for Software Defined Networking (SDN)

With VMM 2016, you can deploy the entire SDN stack using VMM service templates. Leveraging the powerful VMM Service Templates provides you with the capability to deploy and onboard SDN stackthrough a UI-driven and streamlined experience. 

* You can deploy and manage a multi-node Network Controller(NC) in a subnet using VMM Service Templates. After you deploy and onboard the Network Controller, you can configure Network Controller managed fabric to provide connectivity to tenant VMs and to define policies.
* You can deploy and configure a Software Load Balancer to distribute traffic within a network managed by Network Controller. With VMM 2016 Technical Preview release, Software Load Balancer can now also be used for in bound and out bound NAT.
* You can deploy and configure a Windows Server Gateway pool with M+N redundancy using VMM Service Templates. After onboarding Windows Server Gateway, you can connect a tenant network to a hosting provider network or to your own remote data center network using either of the three types of connections supported by Gateway " S2S GRE, S2S IPSec and L3. [Learn more](../Manage/Deploy-a-Software-Defined-Network-infrastructure-using-VMM.md)

### Isolation and filtering of network traffic with access control lists (ACLs) for individual ports

You can limit and segregate network traffic by specifying port ACLs on VM networks, Virtual Subnets, network interfaces, or an entire VMM stamp through the Network Controller using VMM PowerShell cmdlets. [Learn more](https://technet.microsoft.com/library/mt721313%28v=sc.16%29.aspx).

### Consistent naming of virtual network adapters

When you deploy a virtual machine, you might want to run a post-deployment script on the guest operating system to complete the configuration of the virtual network adapters. For example, you might want to configure the Transit network adapter differently from the HNV PA network adapter. Previously, this was tricky, because there wasn't a way to easily distinguish different virtual network adapters at the time of deployment. Now, for generation 2 virtual machines deployed on Hyper-V hosts running Windows Server Technical Preview, you can name the virtual network adapter in a virtual machine template. This is similar to using Consistent Device Naming (CDN) for a physical network adapter.

### Self-service management of an SDN using  Windows Azure Pack (WAP)

In addition to providing parity with WAP support for System Center Virtual Machine Manager 2012 R2, this release will also allow you to provide self service capability for Network Controller managed fabric. Capabilities that can be leveraged through WAP in this Technical Preview include creation and management of VM networks in Network Controller managed fabric, configuration of S2S IPSec connection, and configuring NAT options for tenant and infrastructure Virtual Machines in your data center.  

### Reliable and atomic logical dwitch deployment across hosts

In the previous version of VMM (System Center Virtual Machine Manager 2012 R2), you could collect a variety of individual network settings into a logical switch, so that you could then apply that collection of settings consistently to hosts. In VMM in System Center 2016 Technical Preview, the interface for creating a logical switch has been streamlined to make it easier to see what your choices are and choose settings that will work together.

You can also directly use Hyper-v to configure a standard virtual switch on a managed host, then use VMM to convert the standard virtual switch to a VMM logical switch, and later apply the logical switch to additional hosts.

Also in VMM in System Center 2016 Technical Preview, when you apply a logical switch to a particular host, either the entire operation succeeds, or in the case of failure the operation is reverted and all the settings on the hosts are left unchanged. If Logical switch deployment fails, you can review job information and diagnose reasons for failure through improved logging capability for Logical Switch deployment.

## Security

### Full lifecycle management of guarded hosts and shielded VMs

You can now configure guarded hosts and shielded VMs to help provide protection against malicious host administrators and malware. You can use VMM to manage guarded hosts and shielded VMs in the following ways:

-   After you have installed and configured Host Guardian Service (HGS) server in your environment, you can specify global HGS settings in VMM. You must specify global HGS settings before you configure guarded hosts in your VMM environment.
-   Bring guarded hosts under VMM management. With this release of VMM, the hosts and the VMM server must be in the same domain or in domains with a two-way trust relationship.
-   Configure guarded hosts in your VMM environment to use the global HGS settings that you specified previously.
-   Configure guarded hosts in your VMM environment to use Code Integrity policies. These policies restrict software that can run in kernel mode on a guarded host.
-   View and manage guarded hosts.
-   Create and manage shielded VMs.
-   Convert existing un-shielded VMs to shielded VMs.

[Read more](https://gallery.technet.microsoft.com/Shielded-VMs-and-Guarded-98d2b045) about deploying guarded hosts and managing shielded VMs with VMM.
