---
title: How to install the VMM agent for Linux
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d5c6849-0224-4389-bdc5-86d0ca77a139
---
# How to install the VMM agent for Linux
Before you can use [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] to manage a virtual machine with Linux as the guest operating system, you must install the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] agent for Linux on that virtual machine. Use the following procedure to perform that task.

### To install the VMM agent for Linux on a virtual machine

1.  On the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server, open a command prompt session, with administrative rights.

2.  Go to the ‘c:\\Program Files\\Microsoft System Center 2012\\Virtual Machine Manager\\agents\\Linux’ folder.

3.  Copy all the agent installation files from that folder to a new folder on the virtual machine, and then, on the virtual machine on which Linux is running as a guest operating system, open the new folder.

4.  Run the following command:

    ```
    chmod +x install
    ```

5.  Run either of the following commands, as appropriate:

    ```
    ./install scvmmguestagent.1.0.0.544.x64.tar
    ```

    ```
    ./install scvmmguestagent.1.0.0.544.x86.tar
    ```

The following folders and files are created on the virtual hard disk during the installation of the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] agent for Linux:

-   A default installation folder \- \/opt\/microsoft\/scvmmguestagent

-   A default log files folder \- \/var\/opt\/microsoft\/scvmmagent\/log

-   An installation log file \- scvmm\-install.log

-   A specialization log file \- scvmm.log. This file is created when the virtual machine is deployed and specialized.

-   A configuration file \- scvmm.conf. This file contains the location of the log file and is used to control logging during deployment and specialization.

## See Also
[Requirements for Linux-based virtual machines](Requirements-for-Linux-based-virtual-machines.md)
[Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


