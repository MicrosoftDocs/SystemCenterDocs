---
title: Performing Post-Upgrade Tasks in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f9fdd11-e7e0-43ce-8a40-72fdd61805a3
---
# Performing Post-Upgrade Tasks in VMM
After you complete the [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] upgrade, you may need to make additional configuration changes to your [!INCLUDE[vmm12short](Token/vmm12short_md.md)] environment. For example, you may need to make the following changes:

## <a name="BKMK_Library"></a>Reassociate hosts and library servers
In some upgrade scenarios, you need to reassociate virtual machine hosts and VMM library servers with the VMM management server after the upgrade. For example, you need to reassociate hosts and library servers if you performed the upgrade on a server other than where [!INCLUDE[vmm12short](Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] was installed.

For more information, see [How to Reassociate a Host or Library Server](How-to-Reassociate-a-Host-or-Library-Server.md).

## <a name="BKMK_Agents"></a>Update VMM agents
After the upgrade, you need to update the VMM agents on your Hyper\-V hosts and in your VMM library servers. You do not have to immediately update the VMM agents on Hyper\-V hosts and library servers. The version of the VMM agent that comes with [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] is supported in [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], but it does not provide all of the functionality in [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]. To take advantage of the new functionality, update your VMM agents on your Hyper\-V hosts and library servers.

For more information, see [How to Update the VMM Agent](How-to-Update-the-VMM-Agent.md).

## Configure AlwaysOn Availability Groups
If you upgraded a database that was configured with AlwaysOn Availability Groups, you need to complete a few tasks to ensure that the upgraded database is properly configured with AlwaysOn Availability Groups. For more information, see [How to Complete the Configuration of AlwaysOn Availability Groups for the Database](How-to-Complete-the-Configuration-of-AlwaysOn-Availability-Groups-for-the-Database.md).

## Restore Windows Azure Hyper\-V Recovery Manager
If Windows Azure Hyper\-V Recovery Manager is implemented in the VMM environment, then you need to perform a few steps to restore the Windows Azure Hyper\-V Recovery Manager Provider.

For more information, see [How to Restore Windows Azure Hyper-V Recovery Manager Provider](How-to-Restore-Windows-Azure-Hyper-V-Recovery-Manager-Provider.md).

## <a name="BKMK_Templates"></a>Update virtual machine templates
All virtual machine templates that were upgraded need to correctly specify the virtual hard disk that contains the operating system.

> [!TIP]
> To update a virtual machine template, in the VMM console, open the Library workspace, expand **Templates**, and then click **VM Templates**. In the **Templates** pane, right\-click the virtual machine template that you want to update, click **Properties**, and then go to the **Hardware Configuration** page.

## <a name="BKMK_Drivers"></a>Update driver packages
Driver packages that were previously added to the VMM library must be removed and added again to be correctly discovered.

For more information, see [How to add driver files to the VMM library](How-to-add-driver-files-to-the-VMM-library.md).

## <a name="BKMK_ConfigVMMLibrary"></a>Relocate the VMM library
If you upgraded to a high availability VMM management server, we recommend that you relocate your VMM library to a high availability file server.

For more information, see [Configuring the VMM library](Configuring-the-VMM-library.md).

After you create a new VMM library, you will want to move the resources from the previous VMM library to the new VMM library.

-   To move file\-based resources \(such as ISO images, scripts, and VHDs\), see [How to import and export physical resources to and from the VMM library](How-to-import-and-export-physical-resources-to-and-from-the-VMM-library.md).

-   To move virtual machine templates, see [Exporting and importing service templates in VMM](Exporting-and-importing-service-templates-in-VMM.md).

-   To preserve the custom fields and properties of saved virtual machines in the previous VMM library, deploy the saved virtual machines to a host and then save the virtual machines to the new VMM library.

> [!NOTE]
> Operating system and hardware profiles cannot be moved. You need to re\-create these profiles.

## <a name="BKMK_Additional"></a>Install additional VMM consoles
You can install additional VMM consoles on stand\-alone servers. To connect to a VMM management server that is running [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], you must use the version of the VMM console that comes with [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)].

For more information, see [Installing and Opening the VMM Console](Installing-and-Opening-the-VMM-Console.md).


