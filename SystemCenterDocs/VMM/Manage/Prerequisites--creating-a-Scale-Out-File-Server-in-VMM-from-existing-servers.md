---
title: Prerequisites: creating a Scale-Out File Server in VMM from existing servers
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5244c8e-e3a7-4345-90e4-d103837500c7
---
# Prerequisites: creating a Scale-Out File Server in VMM from existing servers
Before you use [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] to create a Scale\-Out File Server from existing servers, review the prerequisites in this topic. For information about bare\-metal provisioning, or procedures you can follow after meeting these prerequisites, see the links at the end of this topic.

You must meet the following prerequisites for the servers that you will use to create the Scale\-Out File Server:

-   Either the [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] or the [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)] operating system must be installed.

-   The same operating system must be installed on all servers from which the cluster will be created.

-   The servers must all be in the same domain.

You also must have a domain account \(to use as the basis for a Run As account\) for creating the cluster. The account must have administrative permissions on the servers that will become cluster nodes, and must belong to the same domain as those servers. Also, the account requires **Create Computer objects** permission in the container that is used for Computer accounts in the domain. For more information, see the account prerequisites listed in[Create a Failover Cluster](http://technet.microsoft.com/library/dn505754.aspx#BKMK_ClusPrereq).

## See Also
[How to create a Scale-Out File Server in VMM using existing servers](How-to-create-a-Scale-Out-File-Server-in-VMM-using-existing-servers.md)
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


