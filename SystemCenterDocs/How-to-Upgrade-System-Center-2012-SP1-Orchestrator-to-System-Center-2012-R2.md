---
title: How to Upgrade System Center 2012 SP1 Orchestrator to System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4dc4d68-410b-4b9d-a141-49642d6b261c
---
# How to Upgrade System Center 2012 SP1 Orchestrator to System Center 2012 R2
When you upgrade a server that runs [!INCLUDE[orchblue_1](./Token/orchblue_1_md.md)], all features that are installed on the server are upgraded. Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see the [System Requirements](assetId:///aabe0348-a207-46e4-87df-24aa993df984) topic in the [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231) library on TechNet.

#### To upgrade Orchestrator to System Center 2012 R2

1.  Stop all [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] runbooks.

2.  Uninstall the [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] management server, any runbook servers, the Web Service, and the Runbook Designer.

3.  Install the [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] management server in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)], as described in the [Deployment Guide](http://go.microsoft.com/fwlink/?LinkID=232709) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=232709\).

4.  Install any [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] runbook servers in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)].

5.  Install the [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] Runbook Designer in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)].

6.  If needed, install the [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] Web Service in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)].

7.  Take the [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] servers out of maintenance mode.

### Upgrading the integration pack for another System Center 2012 R2 component
The only [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] component for which an updated integration pack is being released for [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] is [!INCLUDE[vmmblue_2](./Token/vmmblue_2_md.md)].

For more detailed instructions for upgrading [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] components, see the guide “Upgrade Sequencing for System Center 2012 R2” that is included in the SC2012R2Upgrade.zip file that you downloaded from the Microsoft Connect website. For each component you will perform the following steps.

1.  Uninstall and unregister the integration pack for the component according to the [How to Uninstall and Unregister an Integration Pack](./How-to-Uninstall-and-Unregister-an-Integration-Pack.md).

    When you install an upgrade of an integration pack, you must first uninstall any earlier version of the integration pack from all runbook servers and Runbook Designers. You then register and deploy the upgrade of the integration pack. If you do not uninstall the previous version of the integration pack prior to registering and deploying the upgrade version, the upgrade version will fail.

2.  Upgrade the component.

3.  Install and register the [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] integration pack for the component.

4.  Verify that [!INCLUDE[orchblue_2](./Token/orchblue_2_md.md)] is receiving data from the component.


