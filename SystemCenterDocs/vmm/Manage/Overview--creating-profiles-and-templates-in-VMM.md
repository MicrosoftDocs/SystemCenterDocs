---
title: Overview: creating profiles and templates in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d894a98d-ac9d-42b3-be7f-aadf23659931
---
# Overview: creating profiles and templates in VMM
In Virtual Machine Manager (VMM), a profile is a “building block” containing some of the specifications that go into creating a new virtual machine or virtual machine template. You can use profiles to simplify the process of creating templates.

Templates help you to quickly create virtual machines with consistent hardware and operating system settings. Templates can also be used to restrict the virtual machine settings that are available to self-service users who create new virtual machines. A virtual machine template typically consists of a hardware profile, an operating system profile, and a virtual hard disk, which will be used by the virtual machine that is created from the template. The virtual hard disk might be stored in the VMM library, or it might be a disk from an existing virtual machine.

## Profiles
VMM provides the following profiles for virtual machine templates:

-   **Hardware profile**—A hardware profile defines hardware configuration settings, such as CPU, memory, network adapters, a video adapter, a DVD drive, and the priority that is given to the virtual machine when resources are allocated on a virtual machine host.

-   **Guest operating system profile**—A guest operating system profile defines operating system configuration settings that will be applied to a virtual machine that is created from the template. It defines common operating system settings, such as the type of operating system, the computer name, administrator password, domain name, product key, time zone, answer file, and RunOnce file.

## Virtual machine templates
Templates are database objects that are stored in the library catalog of the VMM database. Templates are not represented by physical configuration files. Virtual machine templates can be created as follows:

-   From an existing virtual hard disk or virtual machine template that is stored in the library

-   From an existing virtual machine that is deployed on a host

Note that creating a virtual machine template can destroy the virtual machine that is used as the template’s source because Sysprep strips the virtual machine of its computer identity. If you want to continue to use the source virtual machine, clone it before you create the template.

## Services profiles and templates
VMM includes the concept of services, service templates, and a number of profiles that are associated with service templates. Service templates include capabilities not available in virtual machine templates. The following list describes these capabilities:

-   Service templates can be used to deploy multiple virtual machines. Virtual machine templates can be used to deploy a single virtual machine only.

-   Service templates can include settings for installing Windows Server roles and features on virtual machines. If a virtual machine template includes settings for installing roles and features, these settings are only used when the virtual machine is deployed as part of a service.

-   In addition to the standard building blocks of virtual hard disks, hardware profiles, and operating system profiles, service templates can leverage additional profiles that include:

    -   **Application profile**—Application profiles provide instructions that are necessary for installing an application. VMM supports multiple mechanisms for application deployment. Two of these mechanisms are for specific application packaging technologies: data-tier applications (DAC) and WebDeploy, also known as MSDeploy. A third mechanism enables you to install any application by running a script. You can use scripts that are created for Windows Installer (MSI), Setup.exe installation programs, Windows PowerShell Desired State Configuration (DSC), Puppet software, and Chef software.

    -   **SQL Server profile**—SQL Server profiles provide instructions for customizing an instance of Microsoft SQL Server for a SQL Server DAC when a virtual machine is deployed as part of a service.

For more information about service profiles and templates, see [Overview: creating and deploying services in VMM](Overview--creating-and-deploying-services-in-VMM.md).

## See Also
[Creating profiles and templates in VMM](Creating-profiles-and-templates-in-VMM.md)
[Windows PowerShell Desired State Configuration](http://technet.microsoft.com/library/dn249912.aspx)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


