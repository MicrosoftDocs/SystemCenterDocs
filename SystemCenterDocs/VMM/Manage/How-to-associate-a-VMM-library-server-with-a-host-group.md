---
title: How to associate a VMM library server with a host group
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61ab9fda-681f-4c65-ae39-a04f45b1287a
---
# How to associate a VMM library server with a host group
You can use the following procedure to associate a library server with a host group in [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)]. During placement, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] uses this association as an input to help determine which resource to use when a resource with equivalent objects is defined in a profile or template.

**Account requirements** You must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the library server that you want to configure.

### To associate a library server with a host group

1.  Open the **Library** workspace.

2.  In the **Library** pane, expand **Library Servers**, and then click a library server.

3.  On the **Library Server** tab, click **Properties**.

4.  In the *Library Server Name* **Properties** dialog box, in the **Host group** list, click the host group that you want to associate the library server with, and then click **OK**.

    For example, associate the **VMMServer01.contoso.com** library server \(located in Seattle\) with the **Seattle** host group. Associate the **NYLibrary01.contoso.com** library server with the **New York** host group.

    > [!NOTE]
    > You can associate a library server with only one host group. However, child host groups are automatically associated with the library server of the parent host group. Also, realize that you can associate more than one library server with a host group.

## See Also
[How to add a VMM library server or VMM library share](How-to-add-a-VMM-library-server-or-VMM-library-share.md)
[How to add file-based resources to the VMM library](How-to-add-file-based-resources-to-the-VMM-library.md)
[How to create or modify equivalent objects in the VMM library](How-to-create-or-modify-equivalent-objects-in-the-VMM-library.md)
[How to view and remove orphaned resources in VMM](How-to-view-and-remove-orphaned-resources-in-VMM.md)
[Configuring the VMM library](Configuring-the-VMM-library.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


