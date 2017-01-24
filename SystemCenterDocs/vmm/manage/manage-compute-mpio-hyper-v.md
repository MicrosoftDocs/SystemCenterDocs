---
ms.assetid: c3f7b5fa-cb86-4906-b151-24dfbfede61b
title: Manage MPIO for Hyper-V hosts in the VMM fabric
description: This article provides information about managing MPIO for Hyper-V hosts
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  01/23/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Manage MPIO for Hyper-V hosts in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to learn about how System Center 2016 - Virtual Machine Manager (VMM) manages Multipath I/O (MPIO) on Hyper-V hosts.

When you add fiber channel or iSCSI storage to a Hyper-V host managed in the VMM fabirc, he Multipath I/O (MPIO) feature must be enabled on each host.
 - If MPIO is enabled on the host, VMM adds it for [supported storage arrays](../plan/plan-supported-storage-arrays.md) using the Microsoft DSM. If you installed vendor-specific DSMs, then the vendor-specific MPIO settings will be used to connect to the storage array.
 - If you add a host and MPIO isn't enabled, VMM will show a warning message in the **Jobs** window.
 - If you add a host to VMM and enable MPIO afterwards, you need to add the MPIO feature, and then manually configure MPIO to add the discovered device hardware IDs. Alternatively, you can install vendor-specific DSMs.

## MPIO tracking in VMM

When Hyper-V hosts and clusters are added to the VMM fabric, VMM deploys an agent to connectivity between the host and the VMM server. Additionally, VMM collects configuration information about the host or cluster and adds it to VMM. In the case of MPIO, VMM adds two registry keys containing MPIO information.

    - HKEY LOCAL MACHINE\SYSTEM\CurrentControlSet\Control\MPDEV\MPIOSupportedDeviceList
    - HKEY LOCAL MACHINE\SYSTEM\CurrentControlSet\Services\msdsm\Parameters\DsmSupportedDeviceList

After supported storage devices are added to the device list, VMM makes a "claim" on them, and a restart is required on the host. If you've added the host to VMM before deploying workloads on it, then this probably isn't an issue, but if workloads are already running on the host, this could cause interruptions. In an attempt to avoid potential outages, you can run a PowerShell script to prepopulate the MPIO registry keys on a host, before adding it to the VMM fabric. [Learn more](https://blogs.technet.microsoft.com/scvmm/2015/04/30/support-tip-virtual-machine-connections-to-storage-lost-when-adding-host-cluster-in-vmm-2012-r2/) about this script.


## Prevent VMM from claiming device IDs

If you don't want VMM to claim any storage device IDs for MPIO purposes, do the following:

1. Open registry location **HKLM\Software\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings**
2. In this location, create a registry key **RemoveMPIOHardwareIds** with type multi-string.
3. Add the device IDs from the default list. Make sure you use the same spacing.
4. Restart the VMM service.
5. Add the Hyper-V host in the VMM.
