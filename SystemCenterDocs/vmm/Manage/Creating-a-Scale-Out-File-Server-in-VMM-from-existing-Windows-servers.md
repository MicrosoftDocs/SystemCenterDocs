---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Creating a Scale Out File Server in VMM from existing Windows servers
ms.technology:  virtual-machine-manager
ms.assetid:  b1af6ee3-f7a6-4842-8ec0-c3afff8c4bee
---

# Creating a Scale-Out File Server in VMM from existing Windows servers

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

The topics in this section describe the process for using Virtual Machine Manager (VMM) to create a Scale-Out File Server, using existing servers running a Windows Server operating system:

-   [Prerequisites: creating a Scale-Out File Server in VMM from existing servers](Prerequisites--creating-a-Scale-Out-File-Server-in-VMM-from-existing-servers.md)

-   [How to create a Scale-Out File Server in VMM using existing servers](How-to-create-a-Scale-Out-File-Server-in-VMM-using-existing-servers.md)

## <a name="BKMK_workflow"></a>How VMM creates a Scale-Out File Server
During the cluster creation process, after you click **Finish** on the cluster creation wizard, VMM does the following:

1.  Validates that all servers meet the prerequisites, such as required operating system and domain membership

2.  Installs the file server role and the failover cluster feature on each server

3.  Runs the cluster validation process

4.  Creates the cluster and enables the Scale-Out File Server role on the cluster

5.  Adds the provisioned computers as a Scale-Out File Server under VMM management

## See Also
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



