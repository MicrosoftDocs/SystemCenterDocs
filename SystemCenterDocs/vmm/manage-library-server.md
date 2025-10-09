---
ms.assetid: c568f693-0d00-483f-8ffb-099645b31d8e
title: Set up the library in the VMM compute fabric
description: This article provides guidance for setting up the library in the VMM compute fabric
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/02/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Set up the library in the VMM compute fabric




Read this article to understand the System Center Virtual Machine Manager (VMM) library and how to interact with it.


The VMM library is a file share that includes a catalog of resources that are used to deploy virtual machines and services in the VMM fabric. The library stores:

- **File-based resources** such as virtual hard disks, ISO images, and scripts, driver files, and application packages (SQL Server data-tier applications and Web Deploy).
- **Non-file-based resources** such as virtual machine templates and service templates that are used to create VMs and services.
- **Offline virtual machines** are stored in the library.

When you install VMM by default, a single library share is created on the VMM management server. You can add additional shares. For high availability, you can deploy a failover cluster of file servers. Scale out file server (SOFS) isn't supported. You interact with libraries and library resources using the **Library** view in the VMM console.

## What can I do in the library?

Resource type | What can I add?
--- | ---
**File-based resources** | Virtual hard disks (.vhd/.vhdx/.vmdk), ISO image files (.iso) PowerShell scripts (.ps1), SQL Server scripts (.sql), Web Deploy (MSDeploy) packages (.zip), SQL Server data-tier apps - DACS (.dacpac),  driver files (.inf), answer files (.inf, xml), virtual floppy disks (.vfd/.flp)
**Templates and profiles** | Templates help you to quickly create VMs and services with consistent settings. You create and add profiles with specific settings to templates.<br/><br/>**VM templates** are used to create a single VM. A template can be created from an existing virtual hard disk, another VM template in the library, or from a VM deployed on a host.<br/><br/> **Service templates** are used to create multiple VMs and can include settings for Windows Server roles and features. In addition to using hardware and guest OS profiles, service templates can use application and SQL Server profiles.<br/><br/> **Hardware profiles** define hardware settings such as CPU, memory, and priority of VM for resource allocation on host.<br/><br/> **Guest OS profiles** define operating system settings that will be applied when a VM is created from a template. <br/><br/> **Application profiles** provide instructions required to install an app. VMM supports these mechanisms for app deployment - data-tier apps (DAC) and WebDeploy (MSDeploy), running a script created for Windows installer (.msi), setup.exe, Windows PowerShell Desired State Configuration (DSC), Puppet, and Chef.<br/><br/> **SQL Server profiles** provide instructions for customizing a SQL Server instance for a SQL Server DAC.
**Equivalent objects** | Equivalent objects are user-defined groupings of library resources that are considered equivalent. After you've marked objects as equivalent, when you point to a specific virtual disk on a library share in a template or profile, VMM can substitute any equivalent object when a VM or service is created. This means you can author templates and profiles without relying on specific physical resources, and resources can be serviced without affecting the availability of templates and profiles. VMM supports virtual disks, .iso images, and custom resources as equivalent objects.
**Cloud libraries** | Read-only library shares that are assigned to a private cloud and a stored node where self-service users with appropriate permissions can store VMs and services. You can add resources to cloud libraries to make them available for private cloud users.
**Self-service user content** | Self-service users can upload their own resources that can be used when they author templates. Users can share resources with other self-service users.
**Stored VMs and services** | Users can store their VMs that aren't in use in the stored node of the cloud library.
**Update catalog and baselines** | If you manage updates through VMM, then WSUS update baselines are stored in the library.
**Custom resources** | Add custom resources so that resources that would otherwise not be indexed show up in the library. To do this, create a folder with a .CR extension and save it to a library share. Folder contents are available to all users who can access the share. Examples of custom resources include pre- and post-execution scripts and custom installation packages.
**Manage replicated library shares** | You can manage library servers, which are replicated. You can use any replication technologies, such as DFSR, to manage the replicated shares through VMM.

::: moniker range=">=sc-vmm-2019"
Learn more about [managing replicated library shares](library-resources.md#manage-replicated-library-shares).
::: moniker-end

## Next steps

[Learn about adding file-based resources to the library](library-files.md).
