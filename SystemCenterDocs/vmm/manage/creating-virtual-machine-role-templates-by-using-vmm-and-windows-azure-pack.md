---
ms.assetid:  e2581377-1e74-49c1-b02f-1fd245ccd478
title:  Create VM templates using VMM and Windows Azure Pack
description: This article describes how to create VM role templates that can be used by tenants
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Create VM templates using VMM and Windows Azure Pack

>Applies To: System Center 2016 - Virtual Machine Manager

As a hosting provider, you can use VMM in combination with Windows Azure Pack to increase the range of capabilities that you can offer to tenants. To help tenants create virtual machines with specific operating systems and applications already installed, in a way that works flexibly with software licensing methods, you can create Virtual Machine Role templates. Tenants can use these templates to create Virtual Machine Roles in both on-premises hosting environments and service-provider hosting environments.

To begin to create a Virtual Machine Role template, you can download and install one or more Windows Azure Pack Gallery Resources into your hosting environment. Windows Azure Pack Gallery Resources include two types of standard, reusable software packages:

-   Resource Definition package: Forms the basis for creating a virtual machine.

-   Resource Extension package: Forms the basis for installing applications on a virtual machine.

Each Windows Azure Pack Gallery Resource contains a Readme file that explains how to prepare your environment for that resource. Part of the process of installing the gallery resource into your hosting environment is to use Windows PowerShell commands to import the Resource Extension package into VMM.

To create a Virtual Machine Role template, you also need a virtual hard disk file that contains an operating system that has been prepared for deployment. For example, you could use a virtual hard disk file in .vhdx format that contains an operating system such as Windows Server 2012 R2 that has been prepared with the Sysprep tool. After you create the virtual hard disk, you must add it to the VMM library and use the VMM console and Windows PowerShell to provide VMM with necessary information about the virtual hard disk. Examples of this information include the name of the operating system and the specific release number.

Use the following table to find more information about the process for creating a Virtual Machine Role template, and about items such as Windows Azure Pack Gallery Resources, and the Resource Definition and Resource Extension packages within them.

|Type of information|Link|
|-----------------------|--------|
|Information about Windows Azure Pack|[Windows Azure Pack](http://www.microsoft.com/server-cloud/windows-azure-pack.aspx) on the Microsoft website<br /><br />[Windows Azure Pack for Windows Server](http://technet.microsoft.com/library/dn296435.aspx) on TechNet|
|Description of how to add file-based resources, such as virtual hard disk files, to the VMM library|[How to add file-based resources to the VMM library](manage-library-add-files.md) on TechNet|
|Steps for creating a Virtual Machine Role template, including steps for downloading items from the Windows Azure Pack Gallery and steps for importing Resource Extension packages into VMM|[Downloading and Installing Windows Azure Pack Gallery Resource](http://social.technet.microsoft.com/wiki/contents/articles/20194.downloading-and-installing-windows-azure-pack-gallery-resource.aspx) on the TechNet wiki|
|A link for downloading the Web Platform Installer, with which you can download Windows Azure Pack Gallery Resources|[Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx)|
|Description and diagram of how Virtual Machine Role templates are created, with descriptions of Resource Definitions and Resource Extensions|[System Center 2012 R2 Virtual Machine Role Authoring Guide](http://social.technet.microsoft.com/wiki/contents/articles/18272.system-center-2012-r2-virtual-machine-role-authoring-guide.aspx) on the TechNet wiki|
|Steps for creating a customized Virtual Machine Role template, including steps for creating Resource Definition and Resource Extension packages and installing them in your hosting environment|[System Center 2012 R2 Virtual Machine Role Authoring Guide - Installing a Virtual Machine Role](http://social.technet.microsoft.com/wiki/contents/articles/18278.system-center-2012-r2-virtual-machine-role-authoring-guide-installing-a-virtual-machine-role.aspx) on the TechNet wiki|
