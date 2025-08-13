---
ms.assetid: fc72f285-46d9-4a8f-b5e9-187bb6baf781
title: include file
description: include file to detail the new features in virtual machine manager 1807.
author: jyothisuri
ms.author: jsuri
ms.date:  07/24/2018
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
---

## What's new in System Center 1807 - Virtual Machine Manager

See the following sections for information about the new features supported in VMM 1807.

>[!NOTE]
> To view the bugs fixed and the  installation instructions for VMM 1807, see [KB article 4135364](https://support.microsoft.com/help/4135364).


## Storage

### Supports selection of CSV for placing a new VHD

VMM 1807 allows you to select a cluster shared volumes (CSV) for placing a new virtual hard disk (VHD).

In earlier versions of VMM, a new VHD on a virtual machine (VM), by default, is placed on the same CSV where the earlier VHDs associated with the VM are placed, there was no option to choose a different CSV/folder. In case of any issues related to the CSV, such as storage full or overcommitment, users had to migrate the VHD only after deploying the VHD.

With VMM 1807, you can now choose any location to place the new disk. You can manage this disk easily based on the storage availability of CSVs. [Learn more](/previous-versions/system-center/virtual-machine-manager-2008-r2/cc956004(v=technet.10)).

## Networking

### Display of LLDP information for networking devices
 VMM 1807 supports Link Layer Discovery Protocol (LLDP). You can now view network device properties and capabilities information of the hosts from VMM. Host operating system must be Windows 2016 or higher.

 DataCenterBridging and DataCenterBridging-LLDP-Tools features have been enabled on hosts to fetch the LLDP properties.  [Learn more](../vmm/hyper-v-network.md).

### Convert SET switch to logical switch
 VMM 1807 allows you to convert a switch embedded teaming (SET) switch to logical switch by using the VMM console. In earlier versions, this feature was supported only through PowerShell script. [Learn more](../vmm/network-switch.md).

### VMware host management
VMM 1807 supports VMware ESXi v6.5 servers in VMM fabric. This support facilitates the administrators with  additional  flexibility in managing multiple hypervisors in use. [Learn more](../vmm/system-requirements.md#vmware-servers-in-the-vmm-fabric) about the additional details of supported VMware server versions.

### Support for S2D cluster update

VMM 1807 supports update of an S2D host or a cluster. You can update individual S2D hosts or clusters against the baselines configured in windows server update services (WSUS). [Learn more](../vmm/hyper-v-update.md).

## Others

### Support for SQL 2017
VMM 1807 supports SQL 2017. You can upgrade SQL 2016 to 2017.