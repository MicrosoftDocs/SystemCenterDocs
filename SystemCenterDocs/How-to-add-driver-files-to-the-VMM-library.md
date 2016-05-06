---
title: How to add driver files to the VMM library
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e934fc89-0578-4994-b63b-c2582b63eef5
---
# How to add driver files to the VMM library
You can use the following procedures to add driver files to the library in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], and to assign tags to the drivers. After you add driver files to the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library, when you configure a physical computer profile, you can specify the driver files. Then [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can install the specified drivers when it installs the operating system on a physical computer.

In the physical computer profile, you can select to filter the drivers by tags, or you can select to filter drivers with matching Plug and Play \(PnP\) IDs on the physical computer. If you select to filter the drivers by tags, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] determines the drivers to apply by matching the tags that you assign to the drivers in the library to the tags that you assign in the profile. If you select to filter drivers with matching PnP IDs, you do not have to complete the “To assign custom tags to the driver files” procedure in this topic.

> [!NOTE]
> These procedures are optional.

**Account requirements** To add driver files to the library, you must be a member of the Administrator user role, or a member of the Delegated Administrator user role where the management scope includes the library server where the library share is located.

### To add driver files to the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library

1.  Locate a driver package that you want to add to the library.

    For example, you may want to add a driver package for a network adapter driver.

2.  In the library share that is located on the library server that is associated with the group where you want to deploy the physical computers, create a folder to store the drivers, and then copy the driver package to the folder.

    For example, create a folder that is named **Drivers** in the library share, and then copy the driver package for a network adapter driver \(in its own folder\) to the **Drivers** folder.

    > [!IMPORTANT]
    > We strongly recommend that you create a separate folder for each driver package, and that you do not mix resources in the driver folders. If you include other library resources such as .iso images, .vhd files or scripts with an .inf file name extension in the same folder, the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library server will not discover those resources. Also, when you delete an .inf driver package from the library, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] deletes the entire folder where the driver .inf file resides.

3.  In the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, open the **Library** workspace.

4.  In the **Library** pane, expand **Library Servers**, expand the library server where the share is located, right\-click the share, and then click **Refresh**.

    After the library refreshes, the folder that you created to store the drivers appears.

### To assign custom tags to the driver files

1.  In the **Library** pane, expand the folder that you created to store the drivers in the previous procedure, and then click the folder that contains the driver package.

    For example, expand the **Drivers** folder, and then click the folder that you created for the network adapter driver package.

    The driver .inf file of type **Driver Package** is listed in the **Physical Library Objects** pane.

2.  In the **Physical Library Objects** pane, right\-click the driver .inf file, and then click **Properties**.

3.  In the *Driver File Name* **Properties** dialog box, in the **Custom tags** box, enter custom tags separated by a semi\-colon, or click **Select** to assign available tags or to create and assign new ones. If you click **Select**, and then click **New Tag**, you can change the name of the tag after you click **OK**.

    For example, if you added a network adapter driver file, you could create a tag that is named *ServerModel* *NetworkAdapterModel*, where *ServerModel* is the server model and *NetworkAdapterModel* is the network adapter model.

4.  When you are finished, click **OK**.

## See Also
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](../Topic/Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Deploying Scale-Out File Servers from bare metal with VMM](../Topic/Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[How to create a physical computer profile to provision hosts or host cluster nodes from bare metal in VMM](../Topic/How-to-create-a-physical-computer-profile-to-provision-hosts-or-host-cluster-nodes-from-bare-metal-in-VMM.md)
[How to associate a VMM library server with a host group](../Topic/How-to-associate-a-VMM-library-server-with-a-host-group.md)
[Managing infrastructure resources with VMM](../Topic/Managing-infrastructure-resources-with-VMM.md)
[Managing the VMM library and its resources](../Topic/Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

