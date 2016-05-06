---
title: Install DPM as a virtual machine on an on-premises Hyper-V server
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: af0e5e41-bdac-4ce4-9b0a-410cc48e986f
---
# Install DPM as a virtual machine on an on-premises Hyper-V server
You can install DPM 2012 R2 as a virtual machine running on an on\-premises Hyper\-V server. [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] on virtual machines. You run DPM setup as described in [Install System Center 2012 R2 \-  DPM](assetId:///4356a391-57f3-45c4-a108-7c952d99d428), but note the following:

-   Virtual [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] installation is not advised for scaled up environments. Instead, use direct attach\/SAN\-based storage.

-   There is no size limit for VHDX.

-   Both fixed and dynamically expanding VHDX files are supported.

-   Both VHD and VHDX files are supported in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

-   DPM 2012 R2 with Update rollup 3 or later running on as a virtual machine on an on\-premises Hyper\-V host server supports tape drives using synthetic FC.

-   For dynamic and fixed virtual hard drives, VHD and VHDX files are supported on remote SMB shares. Note that a virtual DPM installation is required to support adding virtual hard drives to the storage pool.

-   For high availability [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage, virtual hard drives should be placed on scaled\-out file servers \(SOFS\). Note that SMB 3.0 is required for scaled\-out file servers. For more information, see [Scale\-Out File Server for Application Data overview](http://go.microsoft.com/fwlink/?LinkId=392768). SOFS leverages Windows Server failover clustering and SMB 3.0.

-   Performance can suffer in scaled up \(Hyper\-V on CSV\) environments using VHDX files compared to SAN. Therefore, for scaled up environments we don’t recommend using VHDX.

-   Virtual [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] installations do not support the following:

    -   Windows 2012 Storage Spaces.

    -   Virtual hard drives built on top of storage spaces.

    -   Local or remote hosting of VHDX files on Windows 2012 storage spaces.

    -   Enabling Disk Dedupe on volumes hosting virtual hard drives.

    -   Windows 2012 iSCSI targets \(which use virtual hard drives\) as a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

    -   NTFS compression for volumes hosting VHD files used in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

    -   Bitlocker on volumes hosting VHD files used for the storage pool.

    -   A native 4K sector size of physical disks for VHDX files in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

    -   Virtual hard drives hosted on Windows 2008 servers.


