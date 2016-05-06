---
title: Updating services in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e53faa7-1c16-4a1b-9caf-2e3d22febe91
---
# Updating services in VMM
In [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], updating a service is the process of making changes to a deployed service. Because [!INCLUDE[vmm12short](Token/vmm12short_md.md)] keeps track of which service template was used to deploy a service, you can make updates to the service template, and then use that updated service template to make changes to the deployed service.

[!INCLUDE[vmm12short](Token/vmm12short_md.md)] supports two different methods for making the updates to a deployed service:

-   Applying updates to the existing \(in\-place\) virtual machines

-   Deploying new virtual machines with the updated settings

Applying updates to the existing virtual machines takes less time. Most configuration changes to virtual machines and application updates can be applied in this manner.

To minimize service interruptions when a tier is updated in\-place, you can specify more than one upgrade domain in the tier properties. When the tier is updated, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] updates the virtual machines in the tier according to the upgrade domain to which they belong. [!INCLUDE[vmm12short](Token/vmm12short_md.md)] upgrades one upgrade domain at a time, shutting down the virtual machines running within the upgrade domain, updating them, bringing them back online, and then moving on to the next upgrade domain. By shutting down only the virtual machines running within the current upgrade domain, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] ensures that an upgrade takes place with the least possible impact to the running service. For more information about configuring an upgrade domain, see [How to configure the properties of a service template](How-to-configure-the-properties-of-a-service-template.md).

> [!NOTE]
> Upgrade domains have no connection to Active Directory domains. You can specify the number of upgrade domains you want to use, and then [!INCLUDE[vmm12short](Token/vmm12short_md.md)] arbitrarily assigns the virtual machines to an upgrade domain.

Deploying new virtual machines with the updated settings is a more time\-consuming process, because you are replacing the existing virtual machines of the service with new virtual machines. Typically, this is how you would deploy operating system updates, such as deploying a service pack for the guest operating system on the virtual machine. If you have applications installed on these virtual machines, and your application has a method for saving and restoring application state, you can use a script in the application profile to save the application state before the existing virtual machines are removed and use a script to restore the application state after the new virtual machines have been deployed.

To update a deployed service in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], see the following topics:

-   [How to create an updated service template in VMM](How-to-create-an-updated-service-template-in-VMM.md)

-   [How to update a service template to use an updated resource in VMM](How-to-update-a-service-template-to-use-an-updated-resource-in-VMM.md)

-   [How to apply updates to a deployed service in VMM](How-to-apply-updates-to-a-deployed-service-in-VMM.md)

## See Also
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


