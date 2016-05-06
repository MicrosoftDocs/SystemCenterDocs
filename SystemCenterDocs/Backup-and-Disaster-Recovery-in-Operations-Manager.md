---
title: Backup and Disaster Recovery in Operations Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e265bff-3d30-4f10-80a6-b27d99a4f987
---
# Backup and Disaster Recovery in Operations Manager
As part of your maintenance plan, it is important to include a backup plan. This plan should be thoroughly tested and documented in a simulated environment by using production backups. Ensure that the [!INCLUDE[om12long](../Token/om12long_md.md)] backup plan is integrated in any existing backup procedures in the organization.

> [!NOTE]
> Before reading this section, be sure to review [Planning the System Center 2012 \- Operations Manager Deployment](assetId:///d6edb9b4-5db8-40c2-be00-a32445732d50) to understand the components of [!INCLUDE[om12short](../Token/om12short_md.md)] and to learn how to prepare for failure recovery.

Decide on the following issues:

-   What to back up

-   How often to back up

-   Whether to perform complete or incremental backups

-   How and when to practice restore procedures

After you decide what the best backup strategies for your [!INCLUDE[om12long](../Token/om12long_md.md)] environment, develop and document a backup plan to become part of the overall disaster recovery plan.

We strongly recommend that you test your backup and restore procedures thoroughly. Testing helps ensure that you have the required backups to recover from various failures and that staff can run the procedures smoothly and quickly if a failure occurs.

You can use a test environment including all the [!INCLUDE[om12short](../Token/om12short_md.md)] features to test your backup and restore processes.

> [!NOTE]
> The overall backup practices in your organization might include backing up the disk drives that the [!INCLUDE[om12short](../Token/om12short_md.md)] is installed on. When backing up those disk drives, including the management servers, ensure to exclude the <Installed Partition>\\Program Files\\System Center 2012\\Operations Manager\\Server\\Health Service State folder.

## In This Section
[Complete and Incremental Backups in Operations Manager for System Center 2012](assetId:///c6ec6e61-ad39-4719-9f77-500f56ae0347)

[Backup File Naming Conventions in Operations Manager for System Center 2012](assetId:///6b34b952-8aa3-4e6b-b4c8-5ed665d16896)

[Back Up Operations Manager for System Center 2012](assetId:///b3ffad30-9c3f-45ef-a6da-35c7ac0e58b9)

