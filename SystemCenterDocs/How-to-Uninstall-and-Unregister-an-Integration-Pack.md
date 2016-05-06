---
title: How to Uninstall and Unregister an Integration Pack
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a00f4f58-4fa2-4f7b-803d-1523584a511c
---
# How to Uninstall and Unregister an Integration Pack
For instructions on how to install an integration pack, see the [How To Install an Integration Pack](assetId:///722d2c22-1ea4-4dd0-be22-c662bb0d1473) topic in the [Orchestrator](http://go.microsoft.com/fwlink/?LinkId=264231) library on TechNet.

> [!IMPORTANT]
> When you install an upgrade of an integration pack, you must first uninstall any earlier version of the integration pack from all runbook servers and Runbook Designers. You then register and deploy the upgrade of the integration pack. If you do not uninstall the previous version of the integration pack prior to registering and deploying the upgrade version, the upgrade version will fail.

### To uninstall an integration pack

1.  Open **Programs and Features** in Windows Control Panel.

2.  Right\-click the integration pack and click **Uninstall**.

### To unregister an integration pack

1.  Start the **Deployment Manager**.

2.  In the navigation pane of the Deployment Manager, click **Integration Packs**.

3.  Right\-click the integration pack and click **Unregister Integration Pack or Hotfix from the Orchestrator Management Server**.

## See Also
[Upgrading System Center 2012 SP1 Orchestrator to System Center 2012 R2](../Topic/Upgrading-System-Center-2012-SP1-Orchestrator-to-System-Center-2012-R2.md)

