---
ms.assetid:
description: Include file to summarize the release notes for System Center 2025 - Orchestrator
ms.topic:  include
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.service:  system-center
ms.subservice: Orchestrator
keywords:
ms.date: 07/30/2024
title:  include file
---

## Orchestrator 2025 release notes

The following sections summarize the release notes for Orchestrator 2025, and include all issues fixed until Orchestrator 2022 UR2.

Additionally, the following issues are fixed:

- Send platform event activity is persisted to the database and is visible in **Events** tab of the Runbook Designer.
- Run SSH activity is fixed. Latest (at the time of release) plink.exe is included.
- Query database activity error *Failed to load extension* is fixed.
- Re-create Orchestrator keys by following the steps mentioned [here](/troubleshoot/system-center/orchestrator/license-key-expired-after-migrating-database). 
- Activities persist custom separators while you configure Run behavior for the activity.
- GET api/ActivityInstances returns the expected value instead of empty result.
- Activity names are correctly displayed on the Runbook Tester canvas and log view area instead of identifiers.
- Jobs in active state are visible in Active Jobs in Web Console.

The following sections summarize the known issues and workarounds in System Center Orchestrator 2025:

### Runbooks that aren't inside any folder (root runbooks) aren't shown on the navigation pane

**Workaround**: Move root runbooks to a folder.

### Job form requires output parameter also

**Workaround**: Use any string as value, it will be overwritten by the runbook execution with the output.

### Orchestrator Remoting Service and Runbook Server Monitor Service don’t exit cleanly

**Description**: The *oremoting and omonitor* services can't be stopped using Service kill.

**Workaround**: Kill the service process manually using Task Manager or by using the following command:

```cmd
taskkill /f /pid {pid of the service} 
```
