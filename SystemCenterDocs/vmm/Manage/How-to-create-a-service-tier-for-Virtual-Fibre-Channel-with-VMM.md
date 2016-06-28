---
title: How to create a service tier for Virtual Fibre Channel with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0aca8bc4-197b-4882-956d-72ae89d36720
---
# How to create a service tier for Virtual Fibre Channel with VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

The following is the high-level process for creating a service tier to access Virtual Fibre Channel storage resources.

### To create a service tier for Virtual Fibre Channel

1.  Using the **Service Template Designer**, create a service template and add the applicable VM templates you previously created to the service template.

2.  Add a new Virtual Fibre Channel adapter (vHBA) to the **Configure Hardware** page of the service template. For each vHBA that you create, specify dynamic or static WWPN port assignments and select the fabric classification.

3.  Create service tier from the service template and assign the service tier to a computer tier.

4.  Deploy the tier.

    After you deploy it, you can zone a Virtual Fibre Channel storage array to the service tier. For more information, see [How to manage Virtual Fibre Channel zones and zonesets with VMM](How-to-manage-Virtual-Fibre-Channel-zones-and-zonesets-with-VMM.md). Finally, create a LUN for the array and register (unmask) it to the tier. For more information, see [How to manage storage LUNs for Virtual Fibre Channel with VMM](How-to-manage-storage-LUNs-for-Virtual-Fibre-Channel-with-VMM.md).

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



