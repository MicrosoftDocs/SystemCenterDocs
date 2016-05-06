---
title: How to Upgrade VMM on a Different Computer
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 379a36e9-6811-4190-9f74-69aa590d7e0d
---
# How to Upgrade VMM on a Different Computer
In some cases, you may not want to or may not be able to perform an upgrade on the management server on which [!INCLUDE[vmm12short](Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] is currently installed. For example, you might need to move the VMM database to another computer before beginning the upgrade. In these cases, you can install [!INCLUDE[vmm12short](Token/vmm12short_md.md)] for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] on a different computer, and then use the database from the current [!INCLUDE[vmm12short](Token/vmm12short_md.md)] installation for the upgrade.

Use the following procedure to upgrade [!INCLUDE[vmm12short](Token/vmm12short_md.md)] to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] on a different computer.

> [!CAUTION]
> To avoid any loss of important data, before you upgrade [!INCLUDE[vmm12short](Token/vmm12short_md.md)], we highly recommend that you perform a full backup of your [!INCLUDE[vmm12short](Token/vmm12short_md.md)] database.

### To upgrade VMM to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] on a different computer

1.  Ensure that you have prepared for the upgrade as described in [Planning Considerations for Upgrading VMM](Planning-Considerations-for-Upgrading-VMM.md) and [Tasks to Perform Before Beginning the VMM Upgrade](Tasks-to-Perform-Before-Beginning-the-VMM-Upgrade.md).

2.  Uninstall the current [!INCLUDE[vmm12short](Token/vmm12short_md.md)] deployment. On the **Uninstallation Options** page, select **Retain data**. For more information, see [How to Uninstall VMM](How-to-Uninstall-VMM.md).

3.  Install [!INCLUDE[vmm12short](Token/vmm12short_md.md)] for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] on another computer that meets all the requirements for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)].

4.  During the installation, do the following:

    -   On the **Database configuration** page, specify the VMM database that you retained from the previous [!INCLUDE[vmm12short](Token/vmm12short_md.md)] installation. A message will appear that indicates the selected database was created by a previous version of [!INCLUDE[vmm12short](Token/vmm12short_md.md)]. To upgrade the VMM database, click **OK**.

    -   On the **Configure service account and distributed key management** page, choose your service account and distributed key management settings carefully. Depending on what you choose, encrypted data, like passwords in templates and profiles, may not be available after the upgrade, and you will have to re\-enter them manually. For more information, see [Choosing Service Account and Distributed Key Management Settings During an Upgrade](Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).

After the upgrade, see [Performing Post-Upgrade Tasks in VMM](Performing-Post-Upgrade-Tasks-in-VMM.md).

## See Also
[Performing a VMM Upgrade](Performing-a-VMM-Upgrade.md)
[How to Install a VMM Management Server](How-to-Install-a-VMM-Management-Server.md)


