---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Service Management Automation system runbooks
ms.technology:  service-management-automation
ms.assetid:  f0684cd0-d5e2-43c3-806b-865f42643f0b
---

# Service Management Automation system runbooks

>Applies To: Windows Azure Pack for Windows Server, System Center 2016

The following runbooks ship with Service Management Automation as internal in-system runbooks. They intended to be used only by the Service Management Automation system, and they are not available to be used in the Windows Azure Pack for Windows Server.

## System Runbooks
DiscoverAllLocalModules

-   Runs immediately after a runbook worker is installed

-   Discovers all native modules on the Windows Server system where the runbook worker has been installed, and extracts activities and activity metadata for these modules so that their activities can be used when authoring runbooks in Windows Azure Pack.

SetAutomationModuleActivityMetadata

-   Runs immediately after a module is imported into Service Management Automation

-   Extracts activities and activity metadata from a newly imported module so that its activities can be used when authoring runbooks in Windows Azure Pack.
