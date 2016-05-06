---
title: How to determine the virtual IP address for a service
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 032fe5e4-5da2-4346-ab71-2bba63455f42
---
# How to determine the virtual IP address for a service
In [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], when you deploy a service that is configured to use a hardware load balancer or Microsoft Network Load Balancing \(NLB\), [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] automatically assigns a virtual IP \(VIP\) address to the load balancer from the static IP address pool. The virtual IP address is the address on the load balancer that users will connect to when they access a service.

To enable users to connect to a service, you must determine the virtual IP address that is assigned to the service, and then ask your Domain Name System \(DNS\) administrator to register the address in DNS. For example, the DNS administrator can register the name of *ServiceName*.contoso.com, where *ServiceName* is the name that you want users to specify when they connect to the service.

**Account requirements** To perform this procedure, you must be a full administrator, a delegated administrator, or a read\-only administrator.

### To determine the virtual IP address that is assigned to a service

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **Load Balancers**.

3.  On the **Show** tab, click **Services**.

4.  In the **Load Balancer Information for Services** pane, expand the service with the load\-balanced tier to see which virtual IP address was assigned.

5.  To view more information, click the virtual IP address, and then view the associated information in the details pane.

After you obtain the IP address, ask the DNS administrator to create a DNS entry for the virtual IP address on a DNS server.

## See Also
[How to configure a hardware load balancer for a service tier](../Topic/How-to-configure-a-hardware-load-balancer-for-a-service-tier.md)
[How to configure NLB for a service tier](../Topic/How-to-configure-NLB-for-a-service-tier.md)
[Creating service templates in VMM](../Topic/Creating-service-templates-in-VMM.md)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

