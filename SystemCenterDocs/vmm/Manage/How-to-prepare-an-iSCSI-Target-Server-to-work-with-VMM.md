---
title: How to prepare an iSCSI Target Server to work with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc2f6fee-c93a-437e-8056-5af90dd47ee3
---
# How to prepare an iSCSI Target Server to work with VMM
This topic provides an example of how to prepare a Microsoft iSCSI Target Server to work with System Center 2012 – Virtual Machine Manager (VMM), including how to install the SMI-S provider. 
Note that the VMM management server must be in a domain. The iSCSI Target Server can be in a domain or a workgroup.

### To prepare the example iSCSI-VMM topology

1.  Install VMM on the VMM management server.

    VMM requires Microsoft SQL Server and the Microsoft .NET Framework. If they are not installed, VMM setup prompts you to install them. For more information, see[Preparing your environment for System Center 2016 - Virtual Machine Manager](../Deploy/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md). The Microsoft Standard-based Storage Management service is enabled during VMM installation.

    The VMM installation includes the Microsoft Standard-based Storage Management service (SMS), which will interact with the SMI-S provider.

2.  Install the iSCSI Target Server role.

    One way of doing this is to use the Windows PowerShell command **Install-WindowsFeature FS-iSCSITarget-Server**. iSCSI Target Server is included in the server operating system starting with Windows Server 2012. For more information about using Windows PowerShell to install roles or features, see [Get-WindowsFeature](http://technet.microsoft.com/library/jj205469.aspx) and [Install-WindowsFeature](http://technet.microsoft.com/library/jj205467.aspx).

3.  If needed, install the SMI-S provider.

    This step depends on the version of Windows Server that the iSCSI Target Server runs:

    -   **Windows Server 2012 R2 or later:** Skip this step; the SMI-S provider is installed automatically.

    -   **Windows Server 2012:**

        1.  Install an update rollup no earlier than [Windows 8 and Windows Server 2012 cumulative update: November 2012](http://support.microsoft.com/kb/2770917) (Microsoft KB article 2770917).

            One of the updates in the update rollup contains WMI-related changes to iSCSI Target Server that improve the VMM discovery performance.

        2.  Install the SMI-S provider on it, as follows:

            1.  Find the Setup file in one of the following locations:

                -   On the VMM installation media at:

                    \amd64\Setup\msi\iSCSITargetSMISProvider.msi

                -   On the VMM server at:

                    \Program Files\Microsoft System Center 2012\Virtual Machine Manager\Setup\Msi\iSCSITargetProv\iSCSITargetSMISProvider.msi

            2.  On the iSCSI Target Server, run the .msi file to start the SMI-S Provider Setup wizard.

            3.  Complete the wizard to install the provider.

## See Also
[Configuring iSCSI Target Server and the SMI-S Provider in VMM](Configuring-iSCSI-Target-Server-and-the-SMI-S-Provider-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


