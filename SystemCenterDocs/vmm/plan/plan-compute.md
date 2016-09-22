---
title: Plan the VMM compute fabric
description: This article provides planning steps for setting up and provisioning the VMM compute fabric
author:  rayne-wiselman
ms-author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Plan the VMM compute fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to plan your System Center 2016 - Virtual Machine Manager (VMM) compute fabric. The VMM compute fabric consists of the VMM library, virtualization hosts, host groups, and other infrastructure servers.

## Plan the VMM library

Note the following:

- You should verify system requirements for the VMM library before you install VMM.
- VMM deploys the default library share on the VMM server. After setup is complete you can't remove or relocate the default library share so consider it's location before you install VMM.
- If you're using a SAN the library server should have the same SAN as the hosts that use the library. This ensures that the library server and the hosts can access the same LUNs on the SAN for faster file transfers.
- If you connect to a library from virtualization hosts across a LAN the library server should be as close as possible to the hosts.
- If you're planning to add more library servers you can create library groups to organize them. You can use library groups to align servers with host groups in the VMM fabric. As a best practice you should align each library server with the host group that uses the resources of that library.

## Plan virtualization hosts

VMM supports Hyper-V and VMware virtualization hosts. When you're adding, provisioning, and managing hosts in the VMM fabric consider these points:

- The topology of Hyper-V hosts. VMM can work with Hyper-V hosts that are located in the same domain as the VMM server, in a domain with a two-way trust, or in a domain without a two-way trust. VMM can also work with Hyper-V hosts that are in a perimeter network, or a in disjointed namespace.
- The topology of VMware hosts. VMM can work with VMware hosts located anywhere in your environment.
- The number and type of guest operating systems running on the host.
- The system configuration of the VMs running on the host.
- The types of apps running on the guest operating systems.
- The VM workloads that will run on the host.
- The processor requirements for the host. You'll need enough processing capacity to run the VMs.
- The memory requirements for the host. After you use VMM to allocate host RAM to a VM that memory isn't available for other resources. You also need adequate memory to run the host operating system and any other apps.
- The storage requirements for the host. You need adequate storage for the host itself, as well as for the VMs running on it. Remember you'll need to take extra space into account for VM paging files, dynamically expanding virtual hard disks, saving the contents of VM RAM when the VM is in a saved state, and VM checkpoints.
- The network requirements for the host. If VMs are running apps that need high availability you'll need to consider the network requirements.

## Plan host groups

Host groups act as containers for virtualization hosts and virtual machines. You apply settings at the group level, including setting resources at the host level, specifying hosts for self-service users, and storage and network options. Planning for host groups is especially important in a large-scale deployment, where host groups can help you to effectively manage resource provisioning and management.

You can base your host groups on settings that make sense for your organization. For example:

- For branch offices in your organization.
- To match your Active Directory structure.
- To reflect functions such as development, test, production, or research.
- To limit the hosts used for administrative tasks. For example you could restrict the placement of virtual machines by selecting a particular host group.
- To reserve host resources to determine the CPU, memory, disk space, disk I/O capacity, and network capacity that will always be available to the host operating system.
- To automatically place virtual machines on the most suitable host. Automatic placement is also used to deploy the virtual machines that users create in virtual machine self-service.
- To designate self-service hosts on which users can create and operate their own virtual machines. You add self-service policies to a host group to enable users or groups to create, operate, and manage their own virtual machines within a controlled environment on the hosts in the host group.

Host groups are hierarchical. For example, you can create a child host groups of a existing host group to override host reserves inherited for a parent host group, or to amend VM permissions inherited from the self-service policies of a parent host group.

- All host groups belong to the root host group - All Hosts.
- Each host or host group is identified by its host path, a sequence of host group names that specifies the location of a host or host group within the hierarchy of host groups in the navigation pane. For example, the host path All Hosts\New York\Site21\VMHost05 indicates that the host VMHost05 belongs to the host group Site21, which is a child host group of the host group New York.
- When you change the host reserves for a parent host group, you can choose whether or not to cascade the host reserve settings to hosts in all of its child host groups. If you choose to cascade the host reserve settings, all of the host reserve settings for the parent host group overwrite all previous settings for all hosts in all of the child host groups of the parent host group.
- If a parent host group is used for virtual machine self-service, each of its child host groups automatically inherits self-service policies from the parent host group. However, you can add a self-service policy for the same user or group to both a parent host group and its child host group. By adding policies to both parent and child, you can assign the same users different templates, set different virtual machine permissions, and assign a different virtual machine quota on a subset of hosts within the parent host group.
- You can use a host group to isolate a host. For example, if you have a host with guest operating systems that are running mission-critical applications, you can isolate that host by placing it in its own host group. This way you can ensure that there are no self-service policies applied on the host group and that the system resources set aside for running the host's operating system are appropriate, thus maximizing the host resources available for use by the guest operating systems.

## Next steps

- [Learn about](..deploy/deploy-library-ha.md) deploying the library in high availability mode if required.
- [Manage the VMM library](..manage/manage-library-overview.md)
