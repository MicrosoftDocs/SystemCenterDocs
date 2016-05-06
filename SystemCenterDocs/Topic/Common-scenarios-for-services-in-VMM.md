---
title: Common scenarios for services in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70506004-2c51-4817-a3a0-d86f686279e0
---
# Common scenarios for services in VMM
The following are some common scenarios when using services in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. These scenarios only apply to virtual machines that are deployed as part of service.

|Scenario|Key information|For more information|
|------------|-------------------|------------------------|
|Deploy a virtual machine with Windows Server roles or features installed|-   Must be using at least Windows Server 2008 R2<br />-   Virtual machine must be joined to a domain<br />-   Specify the roles or features to install in a guest operating system profile|[How to create a guest operating system profile](../Topic/How-to-create-a-guest-operating-system-profile.md)|
|Deploy an updated version of the guest operating system \(for example, with the latest service pack\) to a virtual machine|-   Create a new virtual hard disk with the updated operating system<br />-   Create an updated service template<br />-   Update the service by deploying the new virtual machine with the updated settings|[Updating services in VMM](../Topic/Updating-services-in-VMM.md)|
|Deploy a Microsoft Web Deploy application|-   Create a deployment package and add it to the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library<br />-   Create an application profile that specifies the deployment package|[How to Create a Web Deployment Package in Visual Studio](http://msdn.microsoft.com/library/dd465323.aspx)<br /><br />[Configuring the VMM library](../Topic/Configuring-the-VMM-library.md)<br /><br />[How to add file-based resources to the VMM library](../Topic/How-to-add-file-based-resources-to-the-VMM-library.md)<br /><br />[How to create an application profile in a service deployment](../Topic/How-to-create-an-application-profile-in-a-service-deployment.md)|
|Deploy an instance of SQL Server to a virtual machine|-   Create a virtual hard disk that contains a sysprepped version \(prepared instance\) of Microsoft SQL Server. For information about supported versions of Microsoft SQL Server, see [How to create a SQL Server profile in a service deployment](../Topic/How-to-create-a-SQL-Server-profile-in-a-service-deployment.md).<br />-   Create a SQL Server profile.|[How to create a SQL Server profile in a service deployment](../Topic/How-to-create-a-SQL-Server-profile-in-a-service-deployment.md)|

## See Also
[Test Lab Guide for Creating a Service in VMM](http://www.microsoft.com/download/details.aspx?id=38837)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

