---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Managing storage Quality of Service policies for Scale Out File Servers in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  a3b257f9-4e5b-4a2f-bb0b-48ba0fe3448d
---

# Managing storage Quality of Service policies for Scale-Out File Servers in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

The "noisy neighbor" problem is a common problem in virtualized environments. When two virtual machines (VMs) share a resource, say a disk, there is always a chance that one VM"s usage of the resource exceeds that of the other. This might impact the performance of an application running on the VM, as it would not have adequate access to the resource.
## Setting Storage Quality of Service (QOS) Policies
WS 2016 and VMM 2016 introduce the concept of Storage QoS policies to solve the "noisy neighbor" problem. These policies allow the administrator to define the number of Minimum IOPS, Maximum IOPS and Maximum Bandwidth in MB/s. Minimum IOPS is the minimum performance that is guaranteed at any given point in time, whereas Maximum IOPS and Maximum Bandwidth are the performance limits in terms of IOPS and bandwidth that are permissible. You can also set the policy type which defines whether the policy is applicable for a set of VHDs or an individual VHD.

### How to set a Storage QoS for a Scale-out File Server
You can set a Storage QoS policy for a Scale-out file server by following these steps.
1. Create a Storage Quality of Service Policy with the Storage Quality of Service Policy Wizard.
![Create VMM QoS PolicyImage/Create-VMM-QoS-Policy.png)
2. Assign the Storage QoS Policy to a Scale-out File Server volume.
![Assign SOFS PolicyImage/Assign-SOFS-Policy.png)
3. Set the Storage QoS Policy for a Virtual Machine with the Create Virtual Machine Wizard.
![Assign QoS to VMImage/Assign-QoS-to-VM.png)

## See Also
[Understanding virtual machine placement and ratings in VMM](Understanding-virtual-machine-placement-and-ratings-in-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



