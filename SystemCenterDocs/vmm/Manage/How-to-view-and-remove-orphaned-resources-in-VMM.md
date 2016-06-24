---
title: How to view and remove orphaned resources in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd103a0c-a62c-4fb8-8707-97569e4a9ab5
---
# How to view and remove orphaned resources in VMM
You can use the following procedure to view and remove orphaned resources in the Virtual Machine Manager (VMM) library. When you remove a library share from VMM management, and there are templates that reference resources that were located on the library share, a representation of the library resource appears in the VMM library as an orphaned resource.

To remove orphaned resources, you must modify the templates that reference the orphaned resources to use valid library resources in the VMM library. If you re-add the library share, VMM does not automatically re-associate the template with the physical library resource. Therefore, you must still complete the procedures in this topic to correct template issues and to remove any orphaned resources.

**Account requirements** You must be a member of the Administrator user role or a member of the Delegated Administrator role to complete these procedures. Delegated administrators can view and remove only orphaned resources from library shares that were within the scope of their user role. Self-service users do not see the Orphaned Resources node.

### To view and remove orphaned objects

1.  Open the **Library** workspace.

2.  In the **Library** pane, click **Orphaned Resources**.

    Any orphaned resources appear in the Physical Library Objects pane.

    > [!NOTE]
    > You cannot delete an orphaned resource until templates that reference the orphaned resources are updated to reference objects that are in the VMM library.

3.  To view the templates which reference an orphaned resource, right-click the orphaned resource, and then click **Properties**.

4.  In the *Resource Name* **Properties** dialog box, click the **Dependencies** tab.

    The templates that reference the orphaned resource are listed.

5.  To update the template to point to a valid resource, click the template name, and then do the following:

    1.  In the *Template Name* **Properties** dialog box, locate the resource that is missing, and then click **Remove**. For example, if a .vhd file is missing, click **Hardware Configuration**. Under **Bus Configuration**, click the disk that does not have an associated path, and then click **Remove**.

    2.  Add the new resource using a resource that is in the VMM library. For example, add a new disk, click **Browse**, and then click an existing .vhd file.

6.  Repeat step 5 for any other templates that reference the orphaned object.

7.  When you are finished, click **OK** to close the *Orphaned Resource* **Properties** dialog box.

8.  To verify that there are no dependencies, right-click the orphaned resource, and then click **Properties**. Then, click the **Dependencies** tab.

    If there are no dependencies, VMM indicates that no dependencies are found.

9. After you have verified that there are no dependencies, right-click the orphaned resource, and then click **Delete**.

## See Also
[Configuring the VMM library](Configuring-the-VMM-library.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


