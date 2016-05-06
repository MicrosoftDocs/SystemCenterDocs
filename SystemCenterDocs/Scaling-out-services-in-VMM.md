---
title: Scaling out services in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f072eb3a-e695-4e27-b1fb-09400138df03
---
# Scaling out services in VMM
After you have deployed a service in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] and you need to deploy additional virtual machines to a tier of the service, you can use the scale out functionality of [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. For example, during the holiday shopping season, your website may need additional web servers deployed to handle the increase in traffic to your site.

When you create a tier in a service template, you can specify whether that tier can be scaled out and the minimum and maximum number of virtual machines that you can deploy in the tier. For more information, see [How to configure the properties of a service template](./How-to-configure-the-properties-of-a-service-template.md).

If you try to scale out a tier beyond its maximum tier size, you will receive a warning, but [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] will not prevent you from scaling out the tier. However, after the virtual machine is deployed, the tier and the service will show a status of **Needs Attention** in the VMs and Services workspace.

To scale out a tier in a service, see the following topic: [How to scale out a service in VMM](./How-to-scale-out-a-service-in-VMM.md)

## See Also
[Managing services with VMM](./Managing-services-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


