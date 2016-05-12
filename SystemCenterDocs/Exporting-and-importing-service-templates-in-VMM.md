---
title: Exporting and importing service templates in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b28a4e5-cf45-4ad0-8457-e9f8edef9049
---
# Exporting and importing service templates in VMM
In [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], you can export and import service templates.  Exporting and importing service templates gives you the capability to back up service templates and share service templates between different VMM environments.

> [!NOTE]
> You can also export and import virtual machine templates.

When you export a service template in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], tier definitions, hardware settings, guest operating system settings, application installation settings, and network configurations are saved to an .XML file. The export can optionally include sensitive data such as passwords, product keys, and application and global settings that are marked as secure. The sensitive settings can be encrypted. During a service template import, sensitive settings can be included or excluded. If sensitive settings are included, and they were encrypted during the service template export, the encryption password is required.

You can also choose to export some or all of the physical resources \(for example, base virtual hard disks, scripts, or application packages\) that are associated with the service template along with the .XML file for the exported service template. When you import a service template into [!INCLUDE[vmm12short](Token/vmm12short_md.md)], [!INCLUDE[vmm12short](Token/vmm12short_md.md)] validates physical and logical resources that the service template references in the current environment and allows you to update references to missing resources, such as logical resources include logical networks and virtual hard disks.

You can export a service template to a file share or to a [!INCLUDE[vmm12short](Token/vmm12short_md.md)] library share. However, by storing the .XML file on a library share, you can ensure that administrators have access to the file for service template imports.

**Account requirements** In [!INCLUDE[vmm12short](Token/vmm12short_md.md)], administrators can export and import all service templates. Self\-service users whose user role is assigned the **Author** action can export and import service templates that they have access to, irrespective of the owner. When a self\-service user imports a service template, that user becomes the service template owner.

To export and import service templates in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], see the following topics:

-   [How to export a service template in VMM](How-to-export-a-service-template-in-VMM.md)

-   [How to import a service template in VMM](How-to-import-a-service-template-in-VMM.md)

## See Also
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


