---
ms.assetid: 4d983ab4-17dc-4a05-b334-9c2fba69ae82
title: Work with VMM as a self-service user
description: This article describes how to work with VMM as a self-service user
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Work with VMM as a self-service user




This article describes how to work with System Center - Virtual Machine Manager (VMM) as a self-service user.

Self-service users can interact with VMM to deploy virtual machines and services to private clouds. Depending on your permissions, you can deploy VMs from VHDs and templates, and create and share your own templates and profiles. You interact with VMM using the VMM console (or PowerShell).

## Create and deploy virtual machines

- [Learn about](vm-existing-disk.md) creating a VM from an existing VHDs
- [Learn about](vm-blank-disk.md) creating a VM from a blank VHDs
- [Learn about](vm-clone.md) cloning an existing VM
- [Learn about](vm-template.md) deploying VMs from VM templates
- [Learn about](vm-linux.md) deploying VMs running Linux

## Create resources in the VMM library

The VMM library is a file share that includes a catalog of resources that are used to deploy virtual machines and services in the VMM fabric. The library stores:

- File-based resources such as virtual hard disks, ISO images, and scripts, driver files and application packages (SQL Server data-tier applications and Web Deploy).
- Non-file-based resources such as virtual machine templates and service templates that are used to create VMs and services.
- Offline virtual machines are stored in the library.

If you have Author permissions you can create templates and profiles in the library. [Learn more](manage-library-server.md).

### Share library resources

As a self-service user you can share your library resources with other members of your self-service user role when the following conditions are met:

- You must be the resource owner.
- You must belong to self-service user role that has been assigned the Share action.
- To use the shared resource, the user must belong to a self-service user role that has been assigned the Receive action.

Share resources as follows:

1. Click **Library**, right-click the template or physical resource that you want to share > **Properties**.
2. In **Access** > **Users**, click **Add**.
3. In **Select Users**, in User, share the resource with another member of your role. In **User Role**, share the resource with other self-service user roles.


### Import library resources

We recommend you use the method described in this procedure to import and export file-based resources to and from the VMM library. Note the following:

- You can import resource to the user role data path in the Self Service User Content node in the library.
- You can export resources from your user role data path, or private cloud library.
- To import and export your self-service user role needs Author permissions.

Import resources as follows:

1. Click **Library** > **Import** > **Import Physical Resource**.
2. Click **Add custom resource** to import a folder with the .CR extension and its contents. Alternatively, you can select a folder without a .CR extension that contains one or more files of a supported file type.

    - If you select a folder without a .CR extension, only the files of a supported file type will appear in the VMM library.
    - However, if you use Windows Explorer to access the library share, you can access all files in the folder depending on the file and share permissions that are configured outside VMM.
    - If the folder with .CR extension contains more than one hundred file to be imported, it is recommended that you zip the files before the import. This will improve performance.

3. Click **Add resource** to import one or more files to another library location.
4. When you are finished, click **Import**. Check that the resources are listed **Self Service User Content** > user role data path > **Self Service User Objects**.

### Export library resources

1. Click **Library** > **Export** > **Export Physical Resource**.
2. Click **Add** and select the physical resources you want to export. Then click **OK**.
3. In **Specify a destination for the export files**, click **Browse** and select a destination folder. Then click **OK**.
4. When you're finished, click **Export**.

## Next steps

[Provision VMs](provision-vms.md)
