---
title: How to configure the properties of a service template
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b6a1686-44a5-4054-942a-5d721e366907
---
# How to configure the properties of a service template
In [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application.

To prepare to deploy a service, you can configure the following settings in a service template:

-   The service

-   Each tier of the service

-   Networking components \(network adapters and load balancers\)

> [!NOTE]
> The following procedures assume that you have already started to create a service template and that you are working in the Service Template Designer. For information about creating a service template, see [How to create a service template in VMM](./How-to-create-a-service-template-in-VMM.md).

### To configure settings for the service template

1.  On the canvas, select the service template object. The service template object contains the service template name and the release value.

2.  The most common properties that you can change appear in the details pane in the Service Template Designer. To display all of the settings that you can configure, click **View All Properties** in the details pane.

    The following table lists some key settings that you can configure for the service template:

    |Setting|Description|
    |-----------|---------------|
    |**Name**|The name for the service template. This name will appear in the VMs and Services workspace if you deploy a service that is based on this service template.|
    |**Release**|A value to indicate the version of the service template \(for example, **1.0** or **Beta**\).<br /><br />The release value is important for when you update a service. The release value helps you to identify the version of the service template. For more information about updating a service, see [Updating services in VMM](./Updating-services-in-VMM.md).|
    |**Access**|The owner of the service template and a list of self\-service users that can use this service template to deploy a service.|

### To configure settings for a tier

1.  On the canvas, select the tier object.

2.  The most common properties that you can change appear in the details pane in the Service Template Designer. To display all settings that you can configure, click **View All Properties** in the details pane.

    The following table lists some key settings that you can configure for a tier:

    |Setting|Description|
    |-----------|---------------|
    |**Name**|The name for the tier. This name will appear in the **VMs and Services** workspace if you deploy a service that is based on this service template.|
    |**Scale out**|The ability to add additional virtual machines to a tier of a deployed service. For more information about scaling out a tier of a service, see [Scaling out services in VMM](./Scaling-out-services-in-VMM.md).|
    |**Upgrade domains**|A group in which [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically places instances of a tier of a service, so that when the service is updated, those instances are updated at the same time. For more information about updating a service, see [Updating services in VMM](./Updating-services-in-VMM.md).|
    |**Availability set**|A set that contains the virtual machines that you want [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] to keep on separate hosts in order to improve service continuity. When it is possible, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] will separate virtual machines that are in the same availability set, rather than placing them together on one host. For more information about availability sets, see [How to configure availability sets in VMM for virtual machines on a host cluster](./How-to-configure-availability-sets-in-VMM-for-virtual-machines-on-a-host-cluster.md).|
    |**Hardware configuration**|The hardware settings that you want a virtual machine that is deployed in this tier to use. For more information about hardware settings, see [How to create a hardware profile](./How-to-create-a-hardware-profile.md).|
    |**Guest operating system configuration**|The settings of the guest operating system that you want a virtual machine that is deployed in this tier to use. For more information about guest operating system settings, see [How to create a guest operating system profile](./How-to-create-a-guest-operating-system-profile.md).|
    |**Application configuration**|The applications that you want to be installed on a virtual machine that is deployed in this tier. For more information about application installation settings, see [How to create an application profile in a service deployment](./How-to-create-an-application-profile-in-a-service-deployment.md).|
    |**SQL Server configuration**|The instances of SQL Server that you want to be installed on a virtual machine that is deployed in this tier. For more information about installing an instance of SQL Server, see [How to create a SQL Server profile in a service deployment](./How-to-create-a-SQL-Server-profile-in-a-service-deployment.md).|

### To configure settings for a networking component

-   On the canvas, select the networking object that you want to configure.

    For a network adapter, you can configure the following settings:

    -   **IPv4 address type \(dynamic or static\)**

    -   **IPv6 address type \(dynamic or static\)**

    -   **MAC address type \(dynamic or static\)**

    -   **Required bandwidth**

    For a load balancer, you can configure the virtual IP \(VIP\) profile that is being used and provide a description. For more information about adding a load balancer to a tier, see the following topics:

    -   [How to configure a hardware load balancer for a service tier](./How-to-configure-a-hardware-load-balancer-for-a-service-tier.md)

    -   [How to configure NLB for a service tier](./How-to-configure-NLB-for-a-service-tier.md)

## See Also
[Creating service templates in VMM](./Creating-service-templates-in-VMM.md)
[Managing services with VMM](./Managing-services-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


