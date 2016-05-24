---
title: What&#39;s New in VMM in System Center Technical Preview
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2cfb6b1c-1694-4473-bd66-6c0fb91fe167
---
# What&#39;s New in VMM in System Center Technical Preview
This topic describes what's new and changed in Virtual Machine Manager (VMM) in System Center 2016 Technical Preview. The topic includes the following sections:

### [Compute](#bkmkVirtualization)

* Full lifecycle management of newly introduced Nano Server-based hosts and virtual machines (VMs)

-   Rolling Upgrade of a Windows Server 2012 R2 host cluster to Windows Server 2016 with no downtime for the hosted workloads

* Configure bare metal machines as a Hyper-V host cluster in one step instead of two

* Configure bare metal machines as additional nodes of an existing Scale-Out File Server (SOFS) cluster without leaving VMM console

* Increase/decrease memory and add/remove virtual network adapter for a running VM

* Take application-consistent checkpoints, called production checkpoints, of VMs

### [Storage](#bkmkStorage)
* Deploy and manage storage clusters with Storage Spaces Direct (S2D) in dis-aggregated or hyper-converged topology

* Synchronously replicate storage volumes using Storage Replica (SR) instead of expensive storage-based replication

* Set quality of service (QoS) for VM storage to avoid noisy neighbor problem

### [Networking](#bkmkNetworking)

* Template-based deployment for Software Defined Networking (SDN) components such as the Network Controller, Gateway, and Software Load Balancer
* Isolation and filtering of network traffic flowing in and out of a VM vNIC by defining port access control lists (ACLs)

* Consistent naming of virtual network adapters, as seen by the guest operating system

* Self-service capability for Network Controller managed fabric through Windows Azure Pack (WAP)

* Reliable and atomic Logical Switch deployment across hosts

### [Security](#bkmkSecurity)

* Full lifecycle management of newly introduced guarded hosts and shielded VMs

* Convert a non-shielded VM to a shielded VM


## <a name="bkmkVirtualization"></a>Compute


The following Compute enhancements are available in VMM 2016 Technical Preview:

### **Nano Server**

You can now use VMM and perform full lifecycle management of Nano Server-based hosts and virtual machines and leverage the benefits that Nano Server comes with. 

* **Preparing a Nano Server-based host for VMM management**
The very first step in getting started with the lifecycle management of Nano Server is to prepare a Nano Server-based host for VMM. For details, see [How to add a Nano Server as a Hyper-V host in VMM](../Manage/How-to-add-a-Nano-Server-as-a-Hyper-V-host-in-VMM.md)

* **Management of Nano Server-based hosts and clusters (both compute and storage)**
You can now add and manage existing Nano Server-based standalone hosts, compute clusters, and storage clusters (both dis-aggregated and hyper-converged) using VMM. For more details, see [Working with Hyper-V hosts, host clusters and Scale-Out File Servers in VMM](https://technet.microsoft.com/library/mt218831.aspx)

* **Bare metal deployment of Nano Server-based hosts and clusters (both compute and storage)**
You can now configure bare metal machines as Nano Server-based hosts, compute clusters, and storage clusters (both dis-aggregated and hyper-converged). For details regarding bare-metal deployment see [Bare-metal deployment of Hyper-V hosts, host clusters, or Scale-Out File Servers in VMM](https://technet.microsoft.com/library/mt238025.aspx)


### **Cluster Rolling Upgrade** 

You can now upgrade compute or storage clusters from Windows Server 2012 R2 to Windows Server 2016 Technical Preview with no downtime for the host's workloads. VMM orchestrates the entire workflow of draining the node, evicting it, reinstalling the OS, and adding it back to the cluster.


For more details on Cluster Rolling Upgrade in VMM, see [Updating Windows Server 2012 R2 clusters to Windows Server 2016 Technical Preview Clusters in VMM](https://technet.microsoft.com/library/mt445417.aspx)

### **Streamlined workflow for Hyper-V & SOFS Cluster Creation**

With VMM 2016, we have streamlined the creation of Hyper-V host clusters and SOFS clusters and have enabled the below scenarios:

* **Bare metal deployment of Hyper-V Host Clusters**
With VMM 2012 R2, bare metal deployment Hyper-V host cluster was a two-step process.  The 1<sup>st</sup> step was to provision stand-alone Hyper-V hosts from bare metal and the next step was to create a cluster out of these hosts. We have simplified the workflow to be a single step to deploy a Hyper-V host cluster from bare machines. For more details, see [How to deploy a host cluster or Scale-Out File Server cluster from bare metal in VMM](https://technet.microsoft.com/library/mt238029.aspx)

* **Adding a bare-metal node to an existing Hyper-V host cluster or an SOFS Cluster**
With VMM 2016, you can now directly add a bare-metal computer to an existing Hyper-V host cluster or an SOFS Cluster. For more details, see [How to add a bare-metal computer to a host cluster or Scale-Out File Server cluster in VMM](https://technet.microsoft.com/library/mt238035.aspx)

### **New operations for running VMs**

You can now increase/decrease static memory and add/remove virtual network adapter for a running VM. For more details about how to increase or decrease static memory including sample PowerShell scripts, see [Manage Memory for a VM while it is running](../Manage/Manage-Memory-for-a-VM-while-it-is-running.md)
For more information about adding or removing a vNIC see [How to add or remove a vNIC for a running VM](../Manage/How-to-add-or-remove-a-vNIC.md)

### **Production checkpoints** 

You can now create “production checkpoints” for VMs. These checkpoints are based on Volume Shadow Copy Service (VSS) and are application-consistent compared to the “standard checkpoints” that are based on Saved State technology and were not application-consistent.  For more information on production checkpoints see [How to create a production checkpoint for a virtual machine](../Manage/How-to-create-a-production-checkpoint-for-a-virtual-machine.md)

### **Server App-V deprecation in VMM 2016**

Server App-V application in Service Templates is now deprecated in VMM 2016 and you no longer would be able to create a new template or deploy a new service with the Server App-V package. However if you are on VMM 2012 R2 with a service with Server App-V application and are upgrading to VMM 2016, the existing service deployment will continue to work in VMM 2016. This is to ensure that your existing service deployments are not broken post upgrade. Note that post upgrade from VMM 2012 R2 to VMM 2016, you cannot scale out the tier with Server App-V application, however scaling out of other tiers is possible.

## <a name="bkmkStorage"></a>Storage

The following storage enhancements are available in VMM in System Center 2016 Technical Preview:

### **Storage Spaces Direct**: 

Windows Server 2016 Technical Preview introduces Storage Spaces Direct which enables you to build highly available storage system that fit your specific needs, regardless of the exact configuration of your available storage systems. You can use VMM to create a Scale-Out File Server running Windows Server Technical Preview and configure it with Storage Spaces Direct. Then you can create storage pools and file shares on the Scale-Out File Server.

-   For more information, see [Deploying Storage Spaces Direct with VMM](../Manage/Deploying-Storage-Spaces-Direct-with-VMM.md)
-   For information about Storage Spaces Direct, see [Storage Spaces Direct in Windows Server Technical Preview](https://technet.microsoft.com/library/mt126109.aspx)

### **Storage Replica** 

With VMM 2016 you can protect data in a volume by synchronously replicating it to another volume. These two volumes are called the Primary and Recovery volumes. You can deploy the Primary and Secondary volumes either to a single cluster, to two different clusters, or to two stand-alone servers. With VMM 2016 you can use PowerShell to setup Storage Replica between two volumes that are part of a single cluster. Once Storage Replica is setup you can use PowerShell to failover from the Primary Volume to the Recovery Volume.

-   For more information, see [Deploying Storage Replica in VMM](../Manage/Deploying-Storage-Replica-in-VMM.md)
-   For more information about Storage Replica, see [Storage Replica OVerview](https://technet.microsoft.com/library/mt126183.aspx)

### **Quality of Service (QoS) for storage**: 

When hosts and storage are under heavy load, you might want to ensure that certain disks, virtual machines, applications, or tenants will not drop below a certain Quality of Service (QoS) for storage. VMM has been improved so it’s easier to specify QoS. 
- For more information, see [Managing storage Quality of Service for Scale-out file servers in VMM](../Manage/Managing-storage-Quality-of-Service-policies-for-Scale-Out-File-Servers-in-VMM.md)
## <a name="bkmkNetworking"></a>Networking


The following networking enhancements are available in VMM in System Center 2016 Technical Preview:

### **Software Defined Networking**

With VMM 2016, you can deploy the entire Software Defined Networking (SDN) stack using VMM Service Templates. Leveraging the powerful VMM Service Templates provides you with the capability to deploy and onboard SDN stack  through a UI driven and streamlined experience. Following sections cover more details about the SDN artifacts you can deploy using VMM:

* You can deploy and manage a multi-node Network Controller(NC) in a subnet using VMM Service Templates. After you deploy and onboard the Network Controller, you can configure Network Controller managed fabric to provide connectivity to tenant VMs and to define policies.
* You can deploy and configure a Software Load Balancer to distribute traffic within a network managed by Network Controller. With VMM 2016 Technical Preview release, Software Load Balancer can now also be used for in bound and out bound NAT.
* You can deploy and configure a Windows Server Gateway pool with M+N redundancy using VMM Service Templates. After onboarding Windows Server Gateway, you can connect a tenant network to a hosting provider network or to your own remote data center network using either of the three types of connections supported by Gateway – S2S GRE, S2S IPSec and L3.
-   For more information, see [Deploy a Software Defined Network Infrastructure using VMM](../Manage/Deploy-a-Software-Defined-Network-infrastructure-using-VMM.md)

### **Access Control Lists (ACL) for individual ports**

You can limit and segregate network traffic by specifying port ACLs on VM networks, Virtual Subnets, network interfaces, or an entire VMM stamp through the Network Controller using VMM PowerShell cmdlets. 


### **Consistent naming of virtual network adapters**
When you deploy a virtual machine, you might want to run a post-deployment script on the guest operating system to complete the configuration of the virtual network adapters. For example, you might want to configure the Transit network adapter differently from the HNV PA network adapter. Previously, this was tricky, because there wasn’t a way to easily distinguish different virtual network adapters at the time of deployment. Now, for generation 2 virtual machines deployed on Hyper-V hosts running Windows Server Technical Preview, you can name the virtual network adapter in a virtual machine template. This is similar to using Consistent Device Naming (CDN) for a physical network adapter.

### **Self-service management of an SDN through Windows Azure Pack (WAP)**
In addition to providing parity with WAP support for System Center Virtual Machine Manager 2012 R2, this release will also allow you to provide self service capability for Network Controller managed fabric. Capabilities that can be leveraged through WAP in this Technical Preview include creation and management of VM networks in Network Controller managed fabric, configuration of S2S IPSec connection, and configuring NAT options for tenant and infrastructure Virtual Machines in your data center.  

### **Atomic virtual switch deployment**
In the previous version of VMM (System Center Virtual Machine Manager 2012 R2), you could collect a variety of individual network settings into a logical switch, so that you could then apply that collection of settings consistently to hosts. In VMM in System Center 2016 Technical Preview, the interface for creating a logical switch has been streamlined to make it easier to see what your choices are and choose settings that will work together.

You can also directly use Hyper-v to configure a standard virtual switch on a managed host, then use VMM to “convert” the standard virtual switch to a VMM logical switch, and later apply the logical switch to additional hosts.

Also in VMM in System Center 2016 Technical Preview, when you apply a logical switch to a particular host, either the entire operation succeeds, or in the case of failure the operation is reverted and all the settings on the hosts are left unchanged. If Logical switch deployment fails, you can review job information and diagnose reasons for failure through improved logging capability for Logical Switch deployment.



## <a name="bkmkSecurity"></a>Security

You can now configure guarded hosts and shielded VMs to help provide protection against malicious host administrators and malware. You can use VMM to manage guarded hosts and shielded VMs in the following ways:

-   After you have installed and configured Host Guardian Service (HGS) server in your environment, you can specify global HGS settings in VMM. You must specify global HGS settings before you configure guarded hosts in your VMM environment.
-   Bring guarded hosts under VMM management. With this release of VMM, the hosts and the VMM server must be in the same domain or in domains with a two-way trust relationship.
-   Configure guarded hosts in your VMM environment to use the global HGS settings that you specified previously.
-   Configure guarded hosts in your VMM environment to use Code Integrity policies. These policies restrict software that can run in kernel mode on a guarded host.
-   View and manage guarded hosts.
-   Create and manage shielded VMs.
-	Convert existing un-shielded VMs to shielded VMs.

For more information and step-by-step instructions for deploying guarded hosts and managing shielded VMs with VMM see [Shielded VMs and Guarded Fabric Deployment Guide for Windows Server 2016 TP5](https://gallery.technet.microsoft.com/Shielded-VMs-and-Guarded-98d2b045)




