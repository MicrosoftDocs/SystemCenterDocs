---
title: Upgrade to System Center 2012 SP1 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a2b3464-1ff8-4695-875f-839da201c366
---
# Upgrade to System Center 2012 SP1 - Service Manager
You cannot start an upgrade to [!INCLUDE[smlong12](../Token/smlong12_md.md)] SP1 if any data warehouse jobs or workflows are running. You can use the procedures in this section to stop the data warehouse job schedules and wait for them to complete before you upgrade the data warehouse management server. Before you upgrade the [!INCLUDE[smshort](../Token/smshort_md.md)] management server, stop the [!INCLUDE[smssp](../Token/smssp_md.md)], if it is installed, and then wait 10 minutes to let any running workflows finish before you start the upgrade.

Complete the procedures in the following table to upgrade to [!INCLUDE[smlong12](../Token/smlong12_md.md)] SP1.

|Task|Description|
|--------|---------------|
|[How to Prepare Service Manager 2012 for Upgrade to SP1](../Topic/How-to-Prepare-Service-Manager-2012-for-Upgrade-to-SP1.md)|Describes how to stop data warehouse jobs and how to suspend the [!INCLUDE[smssp](../Token/smssp_md.md)].|
|[How to Upgrade to System Center 2012 SP1 - Service Manager](../Topic/How-to-Upgrade-to-System-Center-2012-SP1---Service-Manager.md)|Describes how to upgrade the data warehouse management server, the [!INCLUDE[smshort](../Token/smshort_md.md)] management server, and the [!INCLUDE[smssp](../Token/smssp_md.md)].|

