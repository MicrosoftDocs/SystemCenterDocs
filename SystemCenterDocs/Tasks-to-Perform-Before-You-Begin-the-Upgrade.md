---
title: Tasks to Perform Before You Begin the Upgrade
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 875fed03-5615-4f94-b784-926db2308da2
---
# Tasks to Perform Before You Begin the Upgrade
Before you can upgrade [!INCLUDE[orchblue_2](Token/orchblue_2_md.md)] to [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)], you must prepare the environment by performing the following tasks:

1.  Complete all runbooks running in the current [!INCLUDE[orchblue_2](Token/orchblue_2_md.md)] installation. For information about stopping runbooks, see the [Running Runbooks](Running-Runbooks.md) topic in the [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231) library on TechNet.

2.  Close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using Server Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

3.  Perform a full backup of the [!INCLUDE[orchblue_2](Token/orchblue_2_md.md)] database. For information about backing up the [!INCLUDE[orchblue_2](Token/orchblue_2_md.md)] database, see the [How to Back up Orchestrator](How-to-Back-up-Orchestrator.md) topic in the [Orchestrator](http://go.microsoft.com/fwlink/p/?LinkId=264231) library on TechNet. You can also use tools provided by SQL Server to back up the VMM database. For more information, see [Back Up and Restore of SQL Server Databases](http://go.microsoft.com/fwlink/p/?LinkId=216936).

4.  Upgrade the hardware, operating system, and other software if necessary to meet the requirements of [!INCLUDE[orchblue_2](Token/orchblue_2_md.md)] in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)].

## See Also
[Upgrading System Center 2012 SP1 Orchestrator to System Center 2012 R2](Upgrading-System-Center-2012-SP1-Orchestrator-to-System-Center-2012-R2.md)


