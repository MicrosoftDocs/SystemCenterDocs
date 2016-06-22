---
title: Overview: storage capabilities in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a186e10-14c1-4972-a42b-efe171cf0792
---
# Overview: storage capabilities in VMM
Virtual Machine Manager \(VMM\) recognizes a variety of storage technologies. You can use VMM to configure storage resources to make the most efficient use of your storage technology and capacity.

-   **Discover, configure, and assign storage.** You can use VMM to simplify tasks 
      such as 
        initializing disks
        and formatting new volumes. You can also use VMM to create logical units or file shares, and associate them with hosts or host clusters.
    In addition, you can classify storage to abstract the storage infrastructure.

-   **Use storage capabilities as a factor in virtual machine placement.** When a user deploys a virtual machine, VMM checks the virtual machine template or cloud settings for an assigned storage classification. 
    When VMM rates the potential virtual machine hosts, it prioritizes hosts that have available storage with the appropriate classification.

-   **Deploy virtual machines using the most efficient technology available.** When deploying a virtual machine, VMM must transfer the virtual machine's VHD file from the library to the appropriate storage resource.
    Different storage technologies use different processes for this transfer.
    VMM recognises a number of different storage technologies, and identifies the most efficient process to use for the transfer based on the storage resources involved. For example, if the storage system is a storage area network \(SAN\) that supports Windows Offloaded Data Transfers \(ODX\), VMM uses ODX for the transfer. Otherwise, VMM copies the VHD using another approach such as SMB or BITS.

    > [!NOTE]
    > If accounts are not configured correctly for the VMM library server, hosts, and management processes, VMM uses BITS for the transfer.

    For more information, see [Using SAN copy to rapidly provision virtual machines](Using-SAN-copy-to-rapidly-provision-virtual-machines.md) and [Windows Offloaded Data Transfers Overview](https://technet.microsoft.com/en-us/library/hh831628.aspx).

## Storage technologies supported by VMM
The two broadest categories of storage that VMM recognizes are local and remote storage. Local storage represents storage capacity directly attached to a server \(or on the server\), and is typically used for low\-cost virtualization solutions. Remote storage offloads work from the server to an external storage device where the storage hardware provides scaling and capacity.

VMM supports a number of different types of storage devices such as file servers, storage area networks \(SANs\), and other disk arrays. These devices can define storage capacity in terms of file shares or in terms of blocks identified by logical unit numbers \(LUNs\).

### Block storage
VMM supports block storage devices that connect using Fibre Channel, Serial Attached SCSI \(SAS\), or iSCSI \(Internet SCSI\) connection mechanisms. VMM can discover and manage iSCSI arrays with static, dynamic, or manual targets. Supported technologies include Starwind, HP P2000, Dell EqualLogic, and Microsoft iSCSI Software Target.

VMM also supports thin provisioning, for storage devices that have this capability. Using such storage devices, VMMcan provision logical units as "thick" or "thin;" using thin\-provisioned logical units, you can allocate more capacity to specific applications or users than is physically available in the storage pool.

For more information about integrating VMM with various block storage technologies and configuring block storage, see the following topics:

-   [Configuring iSCSI Target Server and the SMI-S Provider in VMM](Configuring-iSCSI-Target-Server-and-the-SMI-S-Provider-in-VMM.md)

    For more general information about Microsoft iSCSI Target, see [Introduction of iSCSI Target in Windows Server 2012](https://blogs.technet.microsoft.com/filecab/2012/05/21/introduction-of-iscsi-target-in-windows-server-2012/); and
    [Six Uses for the Microsoft iSCSI Software Target](http://blogs.technet.com/b/storageserver/archive/2009/12/11/six-uses-for-the-microsoft-iscsi-software-target.aspx).

-   [Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)

-   [Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)

### File storage
VMM supports devices that used file\-based storage, such as Windows Server file servers. In particular, when you are using Windows Server 2012 Hyper\-V hosts for virtual machines, you can use storage devices that support the Server Message Block \(SMB\) 3.0 network file sharing protocol. Such devices include Scale\-Out File Servers and network\-attached storage \(NAS\) devices from storage vendors such as EMC and NetApp.

For more information, see [Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

### Management interfaces and providers
When installed on Windows Server 2012 or Windows Server 2012 SP1, VMM uses the WMI\-based Storage Management application programming interface \(SMAPI\) to manage storage devices.

SMAPI superseded the Virtual Disk Service \(VDS\) application programming interface \(API\) in Windows Server 2012. 
For more information, see [An Introduction to Storage Management in Windows Server](http://blogs.msdn.com/b/san/archive/2012/06/26/an-introduction-to-storage-management-in-windows-server-2012.aspx).

Using SMAPI, VMM can interact with different storage services and providers, depending on the environment:

-   **SMAPI and Store Management Provider \(SMP\).** VMM can combine SMAPI and SMP to manage directly attached storage and external storage arrays.

-   **SMAPI, Storage Management service, and  Storage Management Initiative Specification \(SMI\-S\).** Vendors of storage devices that follow the SMI\-S standard create SMI\-S providers for their devices.
    The Storage Management service functions as a SMI\-S client.
    VMM can combine SMAPI and the Storage Management service to manage SMI\-S storage devices.

For an example of how VMM can work with storage providers, see [Configuring iSCSI Target Server and the SMI-S Provider in VMM](Configuring-iSCSI-Target-Server-and-the-SMI-S-Provider-in-VMM.md)

## See Also
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


