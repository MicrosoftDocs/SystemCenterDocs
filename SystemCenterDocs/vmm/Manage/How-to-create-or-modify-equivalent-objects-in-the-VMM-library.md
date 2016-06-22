---
title: How to create or modify equivalent objects in the VMM library
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 772a9c9d-a084-40cc-bfbd-2e20af00f5c9
---
# How to create or modify equivalent objects in the VMM library
You can use the following procedures to mark file-based library resources (also known as physical resources) as equivalent objects in Virtual Machine Manager (VMM), and to modify equivalent objects. For example, if you have a Windows Server 2012 R2-based virtual hard disk (.vhd) file that is stored in library shares that are located in two sites, such as Seattle and New York, you can mark the .vhd files as equivalent objects. Then, when you create a template for a new virtual machine, and you specify a .vhd that has equivalent objects, VMM can use any instance of the equivalent object instead of being site-specific. This enables you to use a single template across multiple sites.

> [!IMPORTANT]
> For virtual machine and service deployment, VMM supports only the use of .vhd files, .vhdx files, .iso images, and custom resources as equivalent objects.

> [!NOTE]
> During VMM Setup of a stand-alone VMM management server, Web Deployment Framework custom resources are automatically added to the library as equivalent objects. If you add multiple library shares with the default resources, the framework resources are all automatically marked as equivalent because they share the same family name, release value, and namespace.

**Account requirements** To mark objects as equivalent, you must be a member of the Administrator, Delegated Administrator or Self-Service user roles. Delegated administrators can only mark objects as equivalent on library shares that are within the scope of their user role. Self-service users can only mark objects as equivalent that are in their user role data path in the Self Service User Content node of the VMM library.

### To mark objects as equivalent

1.  Open the **Library** workspace.

2.  In the **Library** pane, click **Library Servers**.

    > [!NOTE]
    > If you are a self-service user, in the **Library** pane, expand **Self Service User Content**, and then click the user role data path.

3.  In the **Physical Library Objects** pane (or the **Self Service User Objects** pane if you are connected as a self-service user), click the **Type** column header to sort the library resources by type.

    > [!NOTE]
    > If you are an administrator or a delegated administrator, the **Library Server** column indicates the location of each resource.

4.  Select the resources that you want to mark as equivalent by using either of the following methods:

    > [!IMPORTANT]
    > The resources that you want to mark as equivalent must be of the same file type. For example, you can mark equivalent .vhd files as equivalent objects, and mark equivalent .iso files as another set of equivalent objects.

    -   Click the first resource, press and hold the CTRL key, and then click the other resources that you want to mark as equivalent.

    -   To select a range, click the first resource in the range, press and hold the SHIFT key, and then click the last resource in the range.

    For example, if you stored a Windows Server 2012 R2-based .vhd file on the Seattle library share that is named **Win2012R2**, and an equivalent .vhd file is located in the New York library share, select both of the .vhd files.

5.  Right-click the selected resources, and then click **Mark Equivalent**.

6.  In the **Equivalent Library Objects** dialog box, do either of the following, and then click **OK**:

    -   If you want to create a new set of equivalent objects, in the **Family** list, type the family name. In the **Release** list, type a release value.

        For example, enter the family name **Windows Server 2012 R2**, and the release value **1.0**.

        > [!NOTE]
        > The value in the **Release** list is a string field. Therefore, you can enter any string value.

    -   If you want to add the resources to an existing set of equivalent objects, in the **Family** list, click an existing family name. In the **Release** list, click the release value.

        The library objects that are considered equivalent are listed in the lower pane.

7.  To verify that the set of equivalent objects was created, in the **Library** pane, click **Equivalent Objects**.

    Verify that the objects that you marked as equivalent appear in the Equivalent Objects pane. They are grouped by family name.

To mark objects as equivalent, the objects must have the same family name, release value, and namespace. The namespace is assigned automatically by VMM. Equivalent objects that are created by an administrator or delegated administrator are assigned the Global namespace. If a self-service user creates equivalent objects within the Self Service User Content node of the Library workspace, VMM assigns a namespace value that matches the name of the self-service user role. This means that a self-service user cannot mark an object as being equivalent with another object that the self-service user role does not own.

### To modify equivalent objects

1.  Open the **Library** workspace.

2.  In the **Library** pane, click **Equivalent Objects**.

3.  In the **Equivalent Objects** pane, expand a family name, expand the release value, right-click the object that you want to modify, and then click **Properties**.

4.  On the **General** tab, modify any of the values, or enter new ones. To remove an object from a set of equivalent objects, delete the family name and release values.

5.  When you are finished, click **OK** to confirm the settings and to close the dialog box.

## See Also
[Configuring the VMM library](Configuring-the-VMM-library.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


