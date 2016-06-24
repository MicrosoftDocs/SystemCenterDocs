---
title: Overview: creating a private cloud with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc4b0684-a9da-4840-b962-77eb6e1398f1
---
# Overview: creating a private cloud with VMM
A private cloud is a cloud that is provisioned and managed on-premises by an organization. The private cloud is deployed by using an organization’s own hardware to leverage the advantages of the private cloud model. By using Virtual Machine Manager (VMM), an organization can manage the private cloud definition and can manage access to the private cloud and the underlying physical resources.

In VMM, a private cloud provides the following benefits:

-   **Self service**—Administrators can delegate management and usage of the private cloud while they retain the opaque usage model. Self-service users do not have to ask the private cloud provider for administrative changes except to request increase capacity and quotas as their requirements change.

-   **Resource pooling**—Through the private cloud, administrators can collect and present an aggregate set of resources, such as storage and networking resources. Resource usage is limited by the capacity of the private cloud and by user role quotas.

-   **Opacity**—Self-service users have no knowledge of the underlying physical resources.

-   **Elasticity**—Administrators can add resources to a private cloud to increase the capacity.

-   **Optimization**—Usage of the underlying resources is continually optimized without affecting the overall private cloud user experience.

You can create a private cloud from either of the following sources:

-   Host groups that contain resources from Hyper-V hosts and VMware ESX hosts

-   A VMware resource pool

During private cloud creation, you select the underlying fabric resources that will be available in the private cloud, configure library paths for private cloud users, and set the capacity for the private cloud. Therefore, before you create a private cloud, you should configure the fabric resources, such as storage, networking, library servers and shares, host groups, and hosts. For information about how to configure the fabric and add hosts to VMM management, see the following sections:

-   [Configuring Fabric Resources in VMM](assetId:///16125788-949e-4caf-a323-a38a224bf2b9)

-   [Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)

-   [VMM support for VMware](VMM-support-for-VMware.md)

## Example scenario overview
In the example scenarios, a private cloud that is named **Finance** is created from resources in configured host groups. A private cloud that is named **Marketing** is created from a VMware resource pool.

The following table summarizes the examples that are used.

> [!NOTE]
> The example resource names and configuration are used to help demonstrate the concepts. The examples build from examples that are used in the "Preparing the Fabric in VMM" section. You can adapt them to your test environment.

|Private cloud|Resource|
|-----------------|------------|
|**Finance**<br /><br />(Private cloud that is created from host groups)|Host groups: **Seattle\Tier0_SEA**, **Seattle\Tier1_SEA**, **New York\Tier0_NY**, **New York\Tier1_NY**<br /><br />Logical network: **Tenants**<br /><br />Load balancer: **LoadBalancer01.contoso.com**<br /><br />Virtual IP profile: **Web tier (HTTPS traffic)**<br /><br />Storage classification: **GOLD** and **SILVER**<br /><br />Read-only library shares: **SEALibrary** and **NYLibrary**<br /><br />Stored virtual machine path: **VMMServer01\Finance\StoredVMs**<br /><br />Capability profile: **Hyper-V**|
|**Marketing**<br /><br />(Private cloud that is created from a VMware resource pool)|VMware resource pool: **Resource pool 1**<br /><br />Logical network: **Tenants**<br /><br />Load balancer: **LoadBalancer01.contoso.com**<br /><br />Virtual IP profile: **Web tier (HTTPS traffic)**<br /><br />Read-only library shares: **SEALibrary** and **NYLibrary**<br /><br />Stored virtual machine path: **VMMServer01\Marketing\StoredVMs**<br /><br />Capability profile: **ESX Server**|

## See Also
[How to create a private cloud from host groups in VMM](How-to-create-a-private-cloud-from-host-groups-in-VMM.md)
[How to create a private cloud from a VMware resource pool in VMM](How-to-create-a-private-cloud-from-a-VMware-resource-pool-in-VMM.md)
[How to increase the capacity of a private cloud in VMM](How-to-increase-the-capacity-of-a-private-cloud-in-VMM.md)
[How to delete a private cloud in VMM](How-to-delete-a-private-cloud-in-VMM.md)
[Managing private clouds with VMM](Managing-private-clouds-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


