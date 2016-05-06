---
title: Creating a Scale-Out File Server in VMM from existing Windows servers
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1af6ee3-f7a6-4842-8ec0-c3afff8c4bee
---
# Creating a Scale-Out File Server in VMM from existing Windows servers
The topics in this section describe the process for using [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] to create a Scale\-Out File Server, using existing servers running a Windows Server operating system:

-   [Prerequisites: creating a Scale-Out File Server in VMM from existing servers](../Topic/Prerequisites--creating-a-Scale-Out-File-Server-in-VMM-from-existing-servers.md)

-   [How to create a Scale-Out File Server in VMM using existing servers](../Topic/How-to-create-a-Scale-Out-File-Server-in-VMM-using-existing-servers.md)

## <a name="BKMK_workflow"></a>How [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] creates a Scale\-Out File Server
During the cluster creation process, after you click **Finish** on the cluster creation wizard, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does the following:

1.  Validates that all servers meet the prerequisites, such as required operating system and domain membership

2.  Installs the file server role and the failover cluster feature on each server

3.  Runs the cluster validation process

4.  Creates the cluster and enables the Scale\-Out File Server role on the cluster

5.  Adds the provisioned computers as a Scale\-Out File Server under [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management

## See Also
[Managing Scale-Out File Servers with VMM](../Topic/Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

