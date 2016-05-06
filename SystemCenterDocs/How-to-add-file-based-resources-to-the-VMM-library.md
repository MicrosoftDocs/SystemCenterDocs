---
title: How to add file-based resources to the VMM library
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0013d379-e4ec-4b19-89d7-86a47c7599d9
---
# How to add file-based resources to the VMM library
You can use the following procedure to add file\-based resources \(such as virtual hard disks and application packages, also known as physical resources\) to an existing library share in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], and then manually refresh the library share. When you add files to a library share, the files do not appear in the library until [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] indexes the files during the next library refresh. By default, the library refresh interval is one hour.

> [!NOTE]
> One hour is the smallest value that you can configure for the library refresh interval. To change the library refresh interval, open the **Library** workspace, and then on the **Home** tab, click **Library Settings**.

For information about the types of file\-based resources that the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library automatically indexes and adds as physical resources, see the table under the “File\-based resources” bullet in [Configuring the VMM library](./Configuring-the-VMM-library.md).

**Account requirements** To add resources to a library share outside [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] or by using the **Explore** option in the Library workspace, a user must have appropriate share and file system permissions assigned outside [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. This applies to administrators, delegated administrators and to self\-service users \(for private cloud library shares\). For information about the account requirements to import and export file\-based resources, see [How to import and export physical resources to and from the VMM library](./How-to-import-and-export-physical-resources-to-and-from-the-VMM-library.md).

### To add file\-based resources to the library

1.  Do any of the following:

    -   Outside [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], browse to the library share, and then copy the files to the share.

    -   In the **Library** workspace of the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, expand **Library Servers**, expand a library server, right\-click a library share, and then click **Explore**. Then, copy files to the share.

    -   In the **Library** workspace of the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, on the **Home** tab, use the **Import Physical Resource** and **Export Physical Resource** options to import and export file\-based resources between library shares. For more information, see [How to import and export physical resources to and from the VMM library](./How-to-import-and-export-physical-resources-to-and-from-the-VMM-library.md).

    For example, copy files that you want to use to the library shares in both sites \(**VMMServer01\\SEALibrary** and **NYLibrary01\\NYLibrary**\).

    > [!NOTE]
    > If you want to create sets of equivalent objects, make sure that you add resources that you consider equivalent to library shares in one or more sites. For example, add a [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)]\-based .vhd file to multiple sites. For information about how to create equivalent objects, see [How to create or modify equivalent objects in the VMM library](./How-to-create-or-modify-equivalent-objects-in-the-VMM-library.md).

2.  To be able to use the files immediately, manually refresh the library share or library server. To do this, follow these steps:

    1.  Open the **Library** workspace.

    2.  In the **Library** pane, expand **Library Servers**, right\-click the library server or library share that you want to refresh, and then click **Refresh**.

    You can open the **Jobs** workspace to view the refresh status.

3.  If the file you added is a virtual hard disk file, as a best practice, provide [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] with important information about that file. This can simplify the process of creating virtual machine templates \(VM templates\) based on the file. To do this:

    1.  In the **Library** workspace, with **Library Servers** expanded, navigate to the library server or library share that contains the file.

    2.  Right\-click the file and then click **Properties**.

    3.  For **Operating system**, expand the list and select the operating system that has been placed on the virtual hard disk.

    4.  Optionally, for **Virtualization platform**, select the virtualization platform on which you will deploy virtual machines that use the file.

    When you have updated the properties, click **OK**.

## See Also
[Configuring the VMM library](./Configuring-the-VMM-library.md)
[How to create or modify equivalent objects in the VMM library](./How-to-create-or-modify-equivalent-objects-in-the-VMM-library.md)
[How to add a VMM library server or VMM library share](./How-to-add-a-VMM-library-server-or-VMM-library-share.md)
[Configuring the VMM library](./Configuring-the-VMM-library.md)
[Managing the VMM library and its resources](./Managing-the-VMM-library-and-its-resources.md)
[Managing Fabric Resources with VMM](Managing-fabric-resources-with-VMM.md)


