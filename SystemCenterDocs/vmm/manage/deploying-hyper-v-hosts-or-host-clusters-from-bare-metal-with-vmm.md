---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Deploying Hyper V hosts or host clusters from bare metal with VMM
ms.technology:  virtual-machine-manager
ms.assetid:  400997d9-08b8-41aa-8af7-72c462e1ea12
---

# Deploying Hyper-V hosts or host clusters from bare metal with VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

As an alternative to adding an existing Hyper-V server or cluster to the VMM fabric you can discover  discover physical bare-metal machines, automatically install an operating system, and provision them as Hyper-V server hosts clusters.

Here's how you do this:

1. **Initial configuration**-Set up the BIOS on the machine to support virtualization, setting the BIOS boot order to boot from a Pre-Boot Execution Environment (PXE)-enabled network adapter as the first device, and configuring the logon credentials and IP address settings for the BMC on each computer. You'll need to create DNS entries and Active Directory account for the machine names, and we recommend you allow time for DNS replication to occur.
2. **Prepare the PXE server environment**:  [Add the PXE server](How-to-add-a-PXE-server-to-VMM.md) to VMM management.
3. **Add resources to VMM library**: Add resources that include a generalized virtual hard disk with an appropriate operating system (as listed in Prerequisites: creating hosts, host clusters, or Scale-Out File Server clusters from bare metal in VMM) that will be used as the base image, and optional driver files to add to the operating system during installation.
4. **Create profiles**: In the library, [create](How-to-create-a-physical-computer-profile-to-provision-hosts-or-host-cluster-nodes-from-bare-metal-in-VMM.md) one or more physical computer profiles. These profiles include configuration settings, such as the location of the operating system image, and hardware and operating system configuration settings.
5. **Create the Hyper-V host or cluster**: You'll run different wizards depending on whether you want to set up a [standalone host](How-to-deploy-Hyper-V-hosts-from-bare-metal-in-VMM.md) or [cluster](How-to-deploy-a-host-cluster-from-bare-metal-in-VMM.md).







 


