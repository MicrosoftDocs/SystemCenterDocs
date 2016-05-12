---
title: Deploying applications with services in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7339ea9a-bbb1-4003-b8cd-61a82948e1bb
---
# Deploying applications with services in VMM
[!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] supports the installation of Microsoft Web Deploy applications and Microsoft SQL Server data\-tier applications \(DACs\), and supports instructions for running scripts when deploying a virtual machine as part of a service. [!INCLUDE[vmm12short](Token/vmm12short_md.md)] also supports installing an instance of SQL Server on to a virtual machine.

## Application framework resources in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]
The Application Frameworks resources available in [!INCLUDE[vmm12short](Token/vmm12short_md.md)] can be used to install tools such as the Web Deployment Tool on a virtual machine and then install applications during service deployment. These resources are available in the VMM library.

The Application Frameworks resources that [!INCLUDE[vmm12short](Token/vmm12short_md.md)] provides include the Microsoft Web Deployment tool, and scripts that can be added to application profiles in service templates to install Web applications during service deployment. One resource, **InstallWebDeploy.cmd**, is used to install the Microsoft Web Deployment tool.

## See Also
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


