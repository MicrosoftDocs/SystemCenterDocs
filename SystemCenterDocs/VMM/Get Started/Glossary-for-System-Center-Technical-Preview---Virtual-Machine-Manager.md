---
title: Glossary for System Center Technical Preview - Virtual Machine Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5cf979fe-a901-4936-a348-ae1fd3b34c7b
---
# Glossary for System Center Technical Preview - Virtual Machine Manager


|Term|Definition|
|--------|--------------|
|Application Frameworks resources|A set of programs, Windows PowerShell cmdlets, and scripts that enable users to install virtual applications and Web applications during the deployment of a service.|
|application profile|A [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] library resource that contains instructions for installing Microsoft Server App\-V, the Web Deploy tool, and Microsoft SQL Server data\-tier applications and for running scripts when you deploy a virtual machine as part of a service.|
|capability profile|A [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library resource that defines which resources \(for example, number of processors or maximum memory\) are available to a virtual machine that is created in a private cloud.|
|cloud library|A grouping of read\-only library shares that are assigned to a private cloud and  a location where self\-service users of a private cloud can store virtual machines or services.|
|dynamic optimization|The capability to perform resource balancing by automatically migrating virtual machines within host clusters that support live migration.|
|equivalent objects|Different files \(for example, .vhd files\) on which a user has set the same family and release properties to indicate that the different files are related.|
|fabric|In [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], the infrastructure resources \(for example, virtual machine hosts, networking, and storage\) that are used to create and deploy virtual machines and services to a private cloud.|
|host profile|A [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library resource that contains hardware and operating system configuration settings to convert a bare\-metal computer to a managed Hyper\-V host.|
|instance count|The number of virtual machines to deploy for a given tier of a service.|
|logical network|A user\-defined named grouping of IP subnets and virtual local area networks \(VLANs\) that is used to organize and simplify network assignments.|
|orphaned resource|A [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library resource on a library server that has been removed from [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], but the resource is still used in a virtual machine template or a service template.|
|physical resource|A file \(for example, .vhd files or script\) that can be imported into or exported from the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library.|
|power optimization|The capability to automatically turn off a virtual host machine that is not needed to meet resource requirements within a host cluster and then turn the virtual host machine back on when it is needed again.|
|private cloud|A grouping of virtual machine hosts and networking, storage, and library resources that is assigned to users to deploy services.|
|Read\-Only Administrator user role|A role that is used to limit users to only viewing status, job status, and properties of objects within their assigned host groups, private clouds, and library servers. A Read\-Only Administrator cannot create new objects.|
|read\-only library share|A library share that is assigned to a private cloud and that is used to share resources to self\-service users that deploy services to that private cloud.|
|scale out \(a service\)|To add additional virtual machines to a tier of a deployed service.|
|Self\-Service User Content|A node in the Library workspace that displays the resources \(for example, .vhd files and scripts\) that self\-service users have uploaded for authoring templates and for sharing with other self\-service users.|
|service|A set of virtual machines that are configured and deployed together and are managed as a single entity. For example, a deployment of a multi\-tier line\-of\-business application.|
|Service Deployment Configurations|A node in the Library workspace where you can view instances of services that have been saved \(during the process of configuring specific deployment settings for the service instance\) but have not been deployed.|
|service template|A [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library resource that contains the configuration settings used to deploy each tier of a service.|
|Service Template Designer|A graphical tool in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console that is used to create and modify service templates.|
|servicing window|A user\-defined time period that can be assigned to a virtual machine, host, or service to indicate when that object is available to be taken offline \(for example, to perform maintenance\).|
|SQL Server profile|A [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library resource that contains instructions for customizing an instance of Microsoft SQL Server for a SQL Server data\-tier application \(DAC\) when you deploy a virtual machine as part of a service.|
|storage classification|A user\-defined name assigned to a storage pool that is used to describe the particular capabilities of the storage pool.|
|tier|An element of a service template that contains the configuration settings necessary to deploy a particular portion of a service.|
|upgrade domain|A group in which [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically places instances of a tier of a service so that when the service is updated, those instances will be updated at the same time.|
|virtual IP template|A template that contains configuration settings for how a load balancer should handle a specific type of network traffic.|

## See Also
[Getting Started with System Center Technical Preview - Virtual Machine Manager](Getting-Started-with-System-Center-Technical-Preview---Virtual-Machine-Manager.md)


