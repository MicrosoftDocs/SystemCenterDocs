---
title: How to create a VM for Virtual Fibre Channel with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b573cc26-2df8-4e9d-97df-406fdab6aa54
---
# How to create a VM for Virtual Fibre Channel with VMM
The following is the high\-level process for creating a virtual machine that can access Virtual Fibre Channel storage resources.

Virtual Host Bus Adapters \(vHBAs\), which represent the virtualization of Fibre Channel HBAs, are used by VMs to connect with vSANs. In order for vHBAs to connect to vSANs, they first must be added to the hardware profile of a VM template.

### To create a VM for Virtual Fibre Channel

1.  Using the  **Create Virtual Machine Wizard**, create a new VM, and then add a new Fibre Channel adapter \(vHBA\) to the **Configure Hardware** page of the VM template. For each vHBA that you create, specify dynamic or static WWPN assignments and select the fabric classification. .

2.  Still using the **Create Virtual Machine Wizard**, place and deploy the VM to a destination host. Make sure the host contains a virtual SAN that matches the storage fabric. .

    After you deploy the VM to a host, you can zone a Virtual Fibre Channel storage array to the VM. For more information, see [How to manage Virtual Fibre Channel zones and zonesets with VMM](How-to-manage-Virtual-Fibre-Channel-zones-and-zonesets-with-VMM.md). Finally, create a LUN and register \(unmask\) it to the VM. For more information, see [How to manage storage LUNs for Virtual Fibre Channel with VMM](How-to-manage-storage-LUNs-for-Virtual-Fibre-Channel-with-VMM.md).

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


