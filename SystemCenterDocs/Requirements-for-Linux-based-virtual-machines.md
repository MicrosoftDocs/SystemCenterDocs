---
title: Requirements for Linux-based virtual machines
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c91336a5-147e-4c9b-9bbc-a0468f9ed945
---
# Requirements for Linux-based virtual machines
[!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] supports virtual machines that contain Linux as the guest operating system. There are several requirements when creating such virtual machines, as follows:

-   Linux Integration Services \(LIS\) must be installed on the virtual machine. By default, LIS is included with some distributions of Linux. If LIS is not included in the distribution of Linux that you are using for the virtual machine, then you must manually install it. For more information about installing LIS for Hyper\-V, see [Linux and FreeBSD Virtual Machines on Hyper-V](http://technet.microsoft.com/library/dn531030.aspx).

-   The [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] guest agent for Linux must be installed on the virtual machine. It is required for service template integration, and it allows you to modify properties on the Linux computer such as the host name. For information about installation, see [How to install the VMM agent for Linux](./How-to-install-the-VMM-agent-for-Linux.md).

[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] does not verify that the virtual machine meets these requirements. However, if these requirements are not met, the virtual machine will fail to deploy.

## See Also
[Creating and deploying virtual machines in VMM](./Creating-and-deploying-virtual-machines-in-VMM.md)
[Managing virtual machines with VMM](./Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


