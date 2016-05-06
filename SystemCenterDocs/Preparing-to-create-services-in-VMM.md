---
title: Preparing to create services in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fb93a2b-2220-47c6-a9db-2961e8e8acdf
---
# Preparing to create services in VMM
Before you begin creating service templates to be used to deploy services in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], you should review and document all the elements that make up the service that you want to deploy. For example:

-   What computers \(physical and virtual\) need to be deployed to support the service?

-   What applications need to be deployed?

-   What networking components are used?

-   Who will use the service?

You also need to ensure that the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] resources needed to deploy the service have been created, configured, and are available. For example:

|Task|For more information|
|--------|------------------------|
|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library resources \(such as virtual hard disks\)|[Configuring the VMM library](../Topic/Configuring-the-VMM-library.md)|
|Networking components \(such as logical networks and load balancers\)|[Configuring Networking in VMM](assetId:///7538ceab-2d04-4fa0-91c7-b66afd0a211d)|
|Virtual machine hosts and host groups|[Overview: using host groups in VMM](../Topic/Overview--using-host-groups-in-VMM.md)<br /><br />[Managing Hyper-V hosts and host clusters with VMM](../Topic/Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)<br /><br />[VMM support for VMware](../Topic/VMM-support-for-VMware.md)|
|Private clouds|[Overview: creating a private cloud with VMM](../Topic/Overview--creating-a-private-cloud-with-VMM.md)|
|Hardware profiles, guest operating system profiles, application profiles, and SQL Server profiles|[Creating profiles and templates in VMM](../Topic/Creating-profiles-and-templates-in-VMM.md)|
|Virtual machine templates|[How to create a virtual machine template](../Topic/How-to-create-a-virtual-machine-template.md)|
|Monitoring and reporting|[Integrating VMM and System Center Operations Manager](../Topic/Integrating-VMM-and-System-Center-Operations-Manager.md)|

-   If you plan to install applications, ensure that you have all the necessary installation files, scripts, and configuration information available for the applications.

-   If you plan to deploy an instance of SQL Server on to a virtual machine, ensure that you have a virtual hard drive that contains a sysprepped version \(prepared instance\) of Microsoft SQL Server. For information about supported versions of Microsoft SQL Server, see [How to create a SQL Server profile in a service deployment](../Topic/How-to-create-a-SQL-Server-profile-in-a-service-deployment.md).

## See Also
[Test Lab Guide for Creating a Service in VMM](http://www.microsoft.com/download/details.aspx?id=38837)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

