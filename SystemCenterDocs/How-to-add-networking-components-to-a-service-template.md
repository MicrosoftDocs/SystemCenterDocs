---
title: How to add networking components to a service template
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3aef573-fc42-4b38-ad19-937b758dac22
---
# How to add networking components to a service template
In [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application.

To prepare to deploy a service, you can add the following networking components to a service template:

-   VM network

-   Load balancer

For information about adding a load balancer to a service template, see the following topics:

-   [How to configure a hardware load balancer for a service tier](How-to-configure-a-hardware-load-balancer-for-a-service-tier.md)

-   [How to configure NLB for a service tier](How-to-configure-NLB-for-a-service-tier.md)

    Note that in service tiers running Linux, or with VM networks configured with network virtualization, you cannot use Microsoft Network Load Balancing \(NLB\). If load balancing is needed for such networks, use hardware load balancing, described in the first item in this list.

-   [How to determine the virtual IP address for a service](How-to-determine-the-virtual-IP-address-for-a-service.md)

> [!IMPORTANT]
> You must configure a load balancer for a tier before you deploy a service. After you deploy a service, you cannot add a load balancer by updating the service.

### To add a VM network to a service template

1.  In the Service Template Designer, on the **Home** tab, in the **Service Template Components** group, click **Add VM Network**. An element representing the VM network is added to the canvas.

2.  Select the VM network element on the canvas, and then in the properties pane at the bottom of the Service Template Designer window, select the appropriate VM network from the **Network** list.

3.  To connect the VM network to the network adapter of a tier, on the **Home** tab, in the **Tools** group, click **Connector**. Then on the canvas, drag from the VM network element to the network adapter element of the tier. A connecting line will appear to join the two elements.

## See Also
[Creating service templates in VMM](Creating-service-templates-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


