---
description: This topic summarizes the supported upgrade scenarios and sequence for System Center 2016. It also includes links to detailed information for upgrading the System Center components.
manager:  cfreeman
ms.topic:  article
author: cfreemanwa
ms.author: cfreeman
ms.prod:  system-center-threshold
keywords:  
ms.date:  10/18/2016
title:  Upgrade-to-System-Center-2016
ms.assetid:  4f8701a5-8d55-4ffd-afee-e6341ec6b7f4
---

# Upgrade to System Center 2016

>Applies To: System Center 2016

If you are already running System Center 2012 R2 you can upgrade your environment to System Center 2016 by following the procedures and guidance in this article. Microsoft only supports upgrading from System Center 2012 R2 from one of the supported update rollup installations listed in the supported upgrade paths sections.


> [!IMPORTANT]
> Make sure you are upgrading to a supported platform by reviewing the [System Requirements topics](../orchestrator/system-requirements.md).

## Supported upgrade paths
Microsoft supports the following upgrade paths.

|Component|Previous Version|
|---------|----------------|
|Data Protection Manager|System Center 2012 R2 with UR10 or later|
|Operations Manager|System Center 2012 R2 with UR9 or later|
|Orchestrator|System Center 2012 R2 with UR8 or later|
|Service Management Automation| System Center 2012 R2 with UR7 or later|
|Service Manager|System Center 2012 R2 with UR9 or later|
|Service Provider Foundation|See the SPF section for details|
|Virtual Machine Manager|System Center 2012 R2 with UR9 or later|

## Upgrade sequence

If you are upgrading an installation of System Center 2012 R2 that includes multiple components, it is important that you upgrade the components in the following order.

1. Service Management Automation
2. Orchestrator
3. Service Manager
4. Data Protection Manager
5. Operations Manager
6. Virtual Machine Manager
7. Service Provider Foundation
8. Windows Azure Pack

## Component Specific Notes

The following topics provide detailed considerations for each component.

-    [Upgrade to System Center 2016 - Data Protection Manager](../dpm/upgrade-to-dpm-2016.md).
-    [Upgrade to System Center 2016 - Operations Manager](../om/deploy/upgrading-to-system-center-2016-operations-manager.md)
-    [Upgrade to System Center 2016 - Orchestrator](../orchestrator/upgrade-to-orchestrator.md)
-    [Upgrade to System Center 2016 - Service Manager](../scsm/upgrade-environment.md)
-    [Upgrade to System Center 2016 - Service Management Automation](../sma/deploy/how-to-upgrade-from-a-previous-version-of-service-management-automation.md)
-    [Upgrade to System Center 2016 - Virtual Machine Manager](../vmm/upgrade.md)
-    [Upgrade to System Center 2016 - Service Provider Foundation](../spf/upgrade.md)
