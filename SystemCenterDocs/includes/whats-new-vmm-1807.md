---
ms.assetid: fc72f285-46d9-4a8f-b5e9-187bb6baf781
title: include file
description: include file to detail the new features in virtual machine manager 1807.
author:  JYOTHIRMAISURI
ms.author: V-jysur
manager:  vvithal
ms.date:  07/24/2018
ms.topic:  include
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

## What's new in System Center 1807 - Virtual Machine Manager

See the following sections for information about the new features supported in VMM 1807.


## Storage
### Supports selection of CSV for placing a new VHD

VMM 1807 allows you to select a cluster shared volumes (CSV) for placing a new virtual hard disc (VHD).

In earlier versions of VMM, a new VHD on a virtual machine (VM), by default, is placed on the same CSV where the earlier VHDs associated with the VM are placed, there was no option to choose a different CSV/ folder. In case of any issues related to the CSV, such as storage full or over commitment, users had to migrate the VHD, only after deploying the VHD.

With VMM 1807, you can now  choose any location to place the new disc. You can manage this disc easily, based on the storage availability of CSVs. [Learn More](../vmm/hyper-v-storage.md).

## Networking

### Display of LLDP information for networking devices
VMM 1807 supports link layer discovery protocol (LLDP). You can now view the properties and capabilities of your network devices through VMM. You can leverage this functionality to remotely monitor the properties of the physical network devices.

DataCenterBridging and DataCenterBridging-LLDP-Tools features have been enabled on the hosts to fetch LLDP properties.  You can view these details through console or PowerShell

**Console view**

To get the details of network devices from the VMM console, go to **View** > **host** > **Properties** > **Hardware Configuration** > **Network adapter**.   

<screenshot to be included in the final location>

> [!NOTE]
> The details displayed contain a time stamp (updated on). To get the current details, refresh the page.

The following LLDP information is displayed:

|**Information displayed** | **Description**
| --- | --- |
| Chassis ID <br/><br/> | Switch chassis identity |
| Port ID <br/><br/> | Switch port ID to which NIC is connected |
| Port Description <br/><br/> | Details related to the connected port |
| System Name	Manufacturer <br/><br/> | Software version details |
| System Description <br/><br/> | Detailed information about the system |
| Available Capabilities <br/><br/> | Available system capabilities (such as switching, routing) |
| Enabled Capabilities <br/><br/> | Enabled system capabilities (such as switching, routing) |
| System Description <br/><br/> | Detailed information about the system |
| Management Address <br/><br/> | IP management address |

**PowerShell**

Use the following PowerShell command to view/refresh the LLDP details:

```powershell
Set-SCVMHostNetworkAdapter -RefreshLLDP
```

> [!NOTE]

> By default, LLDP Packet wait time is set as 30 seconds. You can modify this value by modifying the registry key at **Software\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\LLdpPacketWaitIntervalSeconds**. The minimum value you can set is 5 seconds, maximum value is 300 seconds.


### Convert SET switch to logical switch
 VMM 1807 allows you to convert a switch embedded teaming (SET) switch to logical switch by using the VMM console. In earlier versions. this feature was supported only through PowerShell script. [Learn more](../vmm/network-switch.md)

### VMware host management
VMM 1807 supports VMware ESXi v6.5 servers in VMM fabric. This support facilitates the administrators with  additional  flexibility in managing multiple hypervisors in use. [Learn more](../vmm/system-requirements.md#vmware-servers-in-the-vmm-fabric) about the additional details of supported vmware server versions.

### Support for S2D cluster update

VMM 1807 supports update of an S2D host or a cluster. You can update individual S2D hosts or clusters against the baselines configured in windows server update services (WSUS). [Learn more](../vmm/hyper-v-update.md)
