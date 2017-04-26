---
ms.assetid: c568f693-0d00-483f-8ffb-099645b31d8e
title: Set up the library in the VMM compute fabric
description: This article provides guidance for setting up the library in the VMM compute fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Set up the library in the VMM compute fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to understand the System Center 2016 - Virtual Machine Manager (VMM) library and how you interact with it.


The VMM library is a file share that includes a catalog of resources that are used to deploy virtual machines and services in the VMM fabric. The library stores:

- **File-based resources** such as virtual hard disks, ISO images, and scripts, driver files and application packages (SQL Server data-tier applications and Web Deploy).
- **Non-file-based resources** such as virtual machine templates and service templates that are used to create VMs and services.
- **Offline virtual machines** are stored in the library.

When you install VMM by default a single library share is created on the VMM management server. You can add additional shares.  For high availability you can deploy a failover cluster of file servers. Scale out file server (SOFS) isn't supported. You interact with libraries and library resources using the **Library** view in the VMM console.

## What can I do in the library?

Resource type | What can I add?
--- | ---
**File-based resources** | Virtual hard disks (.vhd/.vhdx/.vmdk), ISO image files (.iso) PowerShell scripts (.ps1), SQL Server scripts (.sql), Web Deploy (MSDeploy) packages (.zip), SQL Server data-tier apps - DACS (.dacpac), Server App-V packages (.osd), driver files (.inf), answer files (.inf, xml), virtual floppy disks (.vfd/.flp)
**Templates and profiles** | Templates help you to quickly create VMs and services with consistent settings. You create and add profiles with specific settings to templates.<br/><br/>**VM templates** are used to created a single VM. A template can be created from an existing virtual hard disk, another VM template in the library, or from a VM deployed on a host.<br/><br/> **Service templates** are used to create multiple VMs and can include settings for Windows Server roles and features. In addition to using hardware and guest OS profiles service templates can leverage application and SQL Server profiles.<br/><br/> **Hardware profiles** define hardware settings such as CPU, memory, priority of VM for resource allocation on host.<br/><br/> **Guest OS profiles** define operating system settings that will be applied when a VM is created from a template. <br/><br/> **Application profiles** provide instructions required to install an app. VMM supports these mechanisms for app deployment - data-tier apps (DAC) and WebDeploy (MSDeploy), running a script created for Windows installer (.msi), setup.exe, Windows PowerShell Desired State Configuration (DSC), Puppet, and Chef.<br/><br/> **SQL Server profiles** provide instructions for customizing a SQL Server instance for a SQL Server DAC.
**Equivalent objects** | Equivalent objects are user-defined groupings of library resources that are considered equivalent. After you've marked objects as equivalent, when you point to a specific virtual disk on a library share in a template or profile, VMM can substitute any equivalent object when a VM or service is created. This means you can author templates and profiles without relying on specific physical resources, and resources can be serviced without affecting the availability of templates and profiles. VMM supports virtual disks, .iso images, and custom resources as equivalent objects.
**Cloud libraries** | Read-only library shares that are assigned to a private cloud and a stored node where self-service users with appropriate permissions can store VMs and services. You can add resources to cloud libraries to make them available for private cloud users.
**Self-service user content** | Self-service users can upload their own resources which can be used when they author templates. Users can share resources with other self-service users.
**Stored VMs and services** | Users can store their VMs that aren't in use in the stored node of the cloud library.
**Update catalog and baselines** | If you manage updates through VMM then WSUS update baselines are stored in the library.
**Custom resources** | Add custom resources so that resources that would otherwise not be indexed show up in the library. To do this you create a folder with a .CR extension and save it to a library share. Folder contents are available to all users who can access the share. Examples for custom resources includes pre and post-execution scripts, and custom installation packages.

## Next steps

[Learn about](library-files.md) adding file-based resources to the library.
