---
title: Overview: creating and deploying services in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43102178-6ebe-4549-88e0-af3a3e29ab18
---
# Overview: creating and deploying services in VMM
In [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application.

In the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, you use the Service Template Designer to create a service template, which defines the configuration of the service. The service template includes information about the virtual machines that are deployed as part of the service, which applications to install on the virtual machines, and the networking configuration needed for the service \(including the use of a load balancer\). The service template can make use of existing virtual machine templates or you can define the service without using any existing virtual machine templates.

After the service template is created, you can then deploy the service to a private cloud or to virtual machine hosts. After the service is deployed, you can update the service template and then deploy those updated changes to the already deployed service. Or you can deploy additional virtual machines to an existing service in order to provide additional resources for the service.

## Why use services?

|Description|Example|
|---------------|-----------|
|Allows you to configure and manage multi\-tier applications as a single entity.|You may have a line\-of\-business application that is comprised of a web server, an application server, and a database server.|
|Enables you to handle fluctuations in capacity for your application, allowing you to easily add or remove virtual machines needed to support the application.|During the holiday shopping season, your website may need additional web servers deployed to handle the increase in traffic to your site.|
|Provides the capability to separate the operating system configuration from the application installation, allowing you to manage fewer operating system images. This also makes updating the application or the underlying operating system easier.|You may need to deploy a new version of an application or apply a service pack to the operating system.|

For more examples of how to use services, see [Common scenarios for services in VMM](../Topic/Common-scenarios-for-services-in-VMM.md).

For a walkthrough of the steps for creating a service, see [Test Lab Guide for Creating a Service in VMM](http://www.microsoft.com/download/details.aspx?id=38837).

## Common tasks for creating and deploying services

|Task|Description|For more information|
|--------|---------------|------------------------|
|Prepare to create services|Ensure that the resources you need to create the service \(for example, virtual machine templates or sequenced applications\) are available before you start|[Preparing to create services in VMM](../Topic/Preparing-to-create-services-in-VMM.md)|
|Create service templates|Use the Service Template Designer to create service templates to deploy services|[Creating service templates in VMM](../Topic/Creating-service-templates-in-VMM.md)|
|Deploy services|Deploy services to private clouds or hosts by using a service template|[Deploying services in VMM](../Topic/Deploying-services-in-VMM.md)|
|Scale out a service|Add additional virtual machines to a deployed service|[Scaling out services in VMM](../Topic/Scaling-out-services-in-VMM.md)|
|Update a service|Make changes to a deployed service|[Updating services in VMM](../Topic/Updating-services-in-VMM.md)|
|Export and import service templates|Backup service templates or copy service templates to another VMM environment|[Exporting and importing service templates in VMM](../Topic/Exporting-and-importing-service-templates-in-VMM.md)|

## See Also
[Test Lab Guide for Creating a Service in VMM](http://www.microsoft.com/download/details.aspx?id=38837)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

