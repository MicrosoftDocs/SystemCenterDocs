---
title: Troubleshooting a VMM Upgrade
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19afef12-e4e8-40c2-aee9-5ea68a71c372
---
# Troubleshooting a VMM Upgrade
For general information about troubleshooting [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], see the[System Center 2012 – Virtual Machine Manager (VMM) General Troubleshooting Guide](http://social.technet.microsoft.com/wiki/contents/articles/8826.system-center-2012-virtual-machine-manager-vmm-general-troubleshooting-guide.aspx) on the TechNet Wiki. Also see the issues listed in [Upgrading to VMM in System Center 2016](Upgrading-to-VMM-in-System-Center-2016.md).

## Log files
If there is a problem when you upgrade [!INCLUDE[vmm12short](Token/vmm12short_md.md)] to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], consult the log files that are located in the **%SYSTEMDRIVE%\\ProgramData\\VMMLogs** folder. Note that the **ProgramData** folder is a hidden folder and you might need to change viewing settings to view this folder.

## Known issues
The following are known issues with a [!INCLUDE[vmm12short](Token/vmm12short_md.md)] upgrade to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]:

-   If multiple errors occur during upgrade, only the first error encountered is shown in the setup wizard. To see all errors that occurred, see the Log files.

## See Also
[Upgrading to VMM in System Center 2016](Upgrading-to-VMM-in-System-Center-2016.md)


