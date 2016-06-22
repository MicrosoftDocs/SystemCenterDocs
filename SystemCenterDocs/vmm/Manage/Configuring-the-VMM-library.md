---
title: Configuring the VMM library
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93ff3733-9789-4b64-96df-10e74034390a
---
# Configuring the VMM library
The procedures in this section describe how to perform basic configuration of the library in Virtual Machine Manager \(VMM\). The VMM library is a catalog of resources that provides access to file\-based resources such as virtual hard disks, virtual floppy disks, ISO images, scripts, driver files and application packages that are stored on library servers, and to non file\-based resources such as virtual machine and service templates and profiles that reside in the VMM database.

The VMM library can store the following types of resources:

-   **File\-based resources**. File\-based resources include virtual hard disks, virtual floppy disks, ISO images, scripts, driver files, and application packages. Application packages include SQL Server data\-tier applications and Web Deploy packages. To be used in VMM, a file must be added to the library. You can also store driver files that are used during the deployment of an operating system when you use VMM to convert a bare\-metal computer to a managed Hyper\-V host.

    > [!NOTE]
    > You can also add custom resources to the library. Custom resources enable you to store resources in the library that would otherwise not be indexed and show up as available resources by the library server. If a user creates a folder with a .CR extension, and then saves the contents to a library share, the folder contents will be available to all users who can access the share. VMM will discover and import the folder into the library as a custom resource. Examples of what you may want to store as a custom resource are pre\- and post\-execution scripts that you want to use for service deployment, or a custom installation package.

    A library server cannot discover files that are associated with a later operating system than the one the library server is running. For example, a library server that is running Windows Server 2008 R2 will not discover .vhdx files because these files did not exist as of Windows Server 2008 R2. The following table lists the file types that are automatically indexed and added as physical library resources during library refreshes in VMM.

    |Library Resource|File Name Extension|
    |--------------------|-----------------------|
    |Virtual hard disks|.vhd and .vhdx \(Hyper\-V\), .vmdk \(VMware\)|
    |ISO image files|.iso|
    |PowerShell scripts|.ps1|
    |SQL Server scripts|.sql|
    |Web Deploy \(MSDeploy\) packages **Note:** These appear in the library as the “Web Application Package” type.|.zip|
    |SQL Server data\-tier applications \(DACs\)|.dacpac|
    |Driver files|.inf **Important:** If you add driver files, we strongly recommend that you create a separate folder for each driver package, and that you do not mix resources in the driver folders. If you include other library resources such as .iso images, .vhd files or scripts with an .inf file name extension in the same folder, the library will not discover those resources. Also, realize that when you delete an .inf driver package from the library, VMM deletes the entire folder where the driver .inf file resides. For more information, see [How to add driver files to the VMM library](How-to-add-driver-files-to-the-VMM-library.md).|
    |Answer files|.inf, .xml|
    |Custom resources|Folders with .CR extension|
    |Virtual floppy disks|.vfd \(Hyper\-V\), .flp \(VMware\)|

    > [!NOTE]
    > Virtual hard disks, ISO images, and virtual floppy disks that are attached to a stored virtual machine, and the configuration files for stored virtual machines, are indexed in VMM but are not displayed as physical resources. The virtual machine configuration files are created by the virtualization software but are not used by VMM. VMM stores a stored virtual machine’s configuration in the VMM database. Virtual machine configuration files include .vmc, .xml, and .vmx \(VMware\) files.

-   **Templates and profiles**. Templates and profiles are used to standardize the creation of virtual machines and services. These configurations are stored in the VMM database but are not represented by physical configuration files. There are several types of templates and profiles in VMM, most of which are used for service creation. There are also host profiles and physical computer profiles, used for deploying a Hyper\-V host from a bare\-metal computer, and capability profiles, used to specify the capabilities of virtual machines on each type of supported hypervisor when virtual machines are deployed to a private cloud.

    > [!NOTE]
    > The VMM library recognizes the .vmtx extension for VMware templates. If you import a VMware template, the template appears under **Templates**, in the **VM Templates** node.

-   **Equivalent objects**. Equivalent objects are a user\-defined grouping of library resources that are considered equivalent. For example, you may mark a Windows Server 2012 R2\-based virtual disk that is located on a library share in Seattle and a Windows Server 2012 R2\-based virtual disk that is located on a library share in New York as equivalent. In a template or profile, when you point to a specific virtual disk on a specific library share, VMM can substitute any equivalent object during virtual machine or service creation. By using equivalent objects, you can author templates or profiles that do not depend on particular physical resources. Therefore, you can service resources without affecting the availability of the template or profile.

    > [!IMPORTANT]
    > For virtual machine and service deployment, VMM supports only the use of virtual disks, .iso images and custom resources as equivalent objects.

    The VMM placement process determines which resource should be used when a resource that has equivalent objects is defined in a profile or template. Placement considers several factors, such as the association between library servers and host groups to help determine which resource to use. This helps to improve performance and optimize network bandwidth usage. Therefore, we recommend that you use resources that have equivalent objects when you create profiles such as application and host profiles, and when you create virtual machine and service templates.

    > [!NOTE]
    > The resources that you mark as equivalent can be files that are replicated by a replication technology or files that you manually copy to each location.

-   **Cloud libraries**. Private cloud libraries consist of read\-only library shares that are assigned to a private cloud and a **Stored Virtual Machines and Services** node where self\-service users who have appropriate permissions can store virtual machines and services. An administrator or a delegated administrator whose management scope includes the library servers can add resources to the read\-only library shares that they want to make available to users of the private cloud.

    During private cloud creation, VMM adds a private cloud library to the **Cloud Libraries** node, with a name that matches the private cloud name. If the administrator specifies read\-only library shares and a path to store virtual machines, the library shares and the **Stored Virtual Machines and Services** nodes appear under the private cloud library. For information about how to create a private cloud, see [Overview: creating a private cloud with VMM](Overview--creating-a-private-cloud-with-VMM.md).

-   **Self\-service user content**. This node enables self\-service users to upload their own resources such as authored templates, virtual disks, ISO image files, application files, scripts and other building blocks to the VMM library. They can use these resources when they author templates. Because this node enables self\-service users to write to a common file path that other members of their user role have access to, self\-service users with appropriate permissions can share resources with other users in the same or a different self\-service user role.

    > [!NOTE]
    > To share with users in a different self\-service user role, the target self\-service user role must have appropriate permissions. For information about how to configure permissions for a self\-service user role, see [How to create a Self-Service User role in VMM](How-to-create-a-Self-Service-User-role-in-VMM.md).

-   **Stored virtual machines and services**. Users can choose to store virtual machines that are not in use to the **Stored Virtual Machines and Services** node. This node is available when you expand **Library Servers**, and then expand the library server.

    > [!NOTE]
    > Be aware that when a self\-service user stores a virtual machine or service to the library, the resource is stored in the **Stored Virtual Machines and Services** node in the private cloud library.

-   **Orphaned resources**. When you remove a library share from VMM management, and there are templates that reference resources that were located on the library share, a representation of the library resource appears in the **Orphaned Resources** node. You can click an orphaned resource to view the templates that reference the orphaned resource. You can then modify the template to reference an existing resource in the VMM library.

-   **Update catalog and baselines**. If you manage updates through VMM for the VMM management server and other computers that are under VMM management, Windows Server Update Services \(WSUS\) update baselines are stored in the VMM library. Updates are covered in more detail in [Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md).

## Operating system requirements
For information about the supported operating systems for the library server role, see[Preparing your environment for System Center 2016 - Virtual Machine Manager](../Deploy/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

## High availability
To make the library server highly available, you can create highly available file shares on a clustered file server that meets the operating system requirements that are outlined in the ‘Operating System Requirements’ section above. For more information about creating failover clusters, see[Create a Failover Cluster](http://technet.microsoft.com/library/dn505754.aspx).

> [!IMPORTANT]
> Do not create highly available file shares for the VMM library on the same cluster as a highly available VMM management server installation. VMM does not support this configuration.

## Example scenario overview
The example scenarios in this section assume that you have a VMM management server installed and a library share configured as part of VMM installation. The scenarios also use a server in a second site that you add as a library server. To demonstrate the concept of equivalent objects, it is best to use multiple library servers and library shares. The following table summarizes the example names that are used in this section.

> [!NOTE]
> The example resource names and configuration are used to help demonstrate the concepts. You can adapt them to your test environment.

|Resource|Resource Name|
|------------|-----------------|
|VMM management server|**VMMServer01.contoso.com**|
|Library share in Seattle \(added during VMM management server installation\)|**VMMServer01\\SEALibrary**|
|Library server and share in New York|**NYLibrary01\\NYLibrary**|

## In This Section
Use the following procedures to perform basic configuration of the VMM library.

|Procedure|Description|
|-------------|---------------|
|[How to add a VMM library server or VMM library share](How-to-add-a-VMM-library-server-or-VMM-library-share.md)|Describes how to add a new library server or library share.|
|[How to associate a VMM library server with a host group](How-to-associate-a-VMM-library-server-with-a-host-group.md)|Describes how to associate a library server with a host group. This association helps VMM to determine which resource to use when there is a set of equivalent objects.|
|[How to add file-based resources to the VMM library](How-to-add-file-based-resources-to-the-VMM-library.md)|Describes how to add file\-based resources to the library.|
|[How to create or modify equivalent objects in the VMM library](How-to-create-or-modify-equivalent-objects-in-the-VMM-library.md)|Describes how to mark file\-based objects as equivalent.|
|[How to view and remove orphaned resources in VMM](How-to-view-and-remove-orphaned-resources-in-VMM.md)|Describes how to view orphaned resources, and how to resolve any issues with templates that reference the orphaned resource so that you can remove the orphaned resource.|

## See Also
[How to add driver files to the VMM library](How-to-add-driver-files-to-the-VMM-library.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


