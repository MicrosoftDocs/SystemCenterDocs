---
ms.assetid: ac25266c-9def-404d-95dc-6d037fb710e4
title: include file
description: include file to summarize the release notes for VMM 2019.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  02/11/2019
ms.topic:  include
ms.prod:  system-center
ms.technology:  virtual-machine-manager
---

## VMM 2019 release notes

The following sections summarize the release notes for VMM 2019 and include the known issues and workarounds.

## Removal of cluster node fails with CleanUpDisks flag

 **Description**: When you remove a cluster node from Windows Server 2019 S2D cluster, with a CleanUpDisks flag, the removal fails with **Could not get the specified instance MSFT_StorageJob** error, in the following scenarios

  - The storage capacity is inadequate in the remaining servers to accommodate all the volumes.

  - There are not enough fault domains to provide the resiliency of the volume.  

**Workaround**: Ensure the following:

-  Adequate storage capacity is available in the remaining servers to accommodate all the volumes

-  Enough fault domains are available to provide the resiliency of your volumes.  

## Addition of storage device with SMI-S management interface fails

**Description**: Addition of storage device having SMI-S management interface fails with the error **Registration of storage provider failed with error code WsManMIInvokeFailed** when System Center Virtual Machine Manager 2019 is installed on Windows Server 2019.  

**Workaround**: VMM depends on the **Windows Standards-Based Storage Management** service to manage the storage devices using SMI-S. Make sure that the service is started before trying to add the storage device.  

## Windows Server 2019 does not support HNVv1 networks

**Description**: Windows Server 2019 does not support HNVv1. If HNVv1 is currently in use, then the cluster that is utilizing HNVv1 should not be upgraded to Windows Server 2019 using Cluster Rolling Upgrade.

**Workaround**: Migrate out of HNVv1 to SDNv2 on Windows Server 2016 before using Cluster Rolling upgrade to Windows Server 2019.

## Latest accessibility fixes in Console are not available

**Description**: Latest accessibility fixes in Console might not be available when you use .NET 4.7 while installing the VMM console.

**Workaround**: We recommend using .NET 4.7.1 while installing the VMM Console. For detailed information on .NET 4.7.1 migration, see [the article on .NET migration
 ](https://docs.microsoft.com/dotnet/framework/migration-guide/retargeting/4.7-4.7.1).    

## Backend adapter connectivity for SLB MUX doesn't work as expected

**Description**: Backend adapter connectivity of SLB MUX might not work as expected after VM migration.

**Workaround**: Users scale in/scale out in the SLB MUX VM as a workaround.
