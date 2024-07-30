---
ms.assetid:
description: include file to summarize the release notes for System Center 2025 - Orchestrator
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

The following sections summarizes the release notes for Orchestrator 2025, and includes all issues fixed until SCO 2022 UR2.

Additionally, the following issues have been fixed:

- Send platform event activity is persisted to the database and is visible in **Events** tab of the Runbook Designer.
- System Center Orchestrator now supports Group Managed Service Accounts (gMSA).

The following sections summarize the known issues and workarounds in SCO 2025:

### Activity inside a runbook instance returns an empty set

**Description**:  Direct calls to GET api/ActivityInstances or selecting an activity inside a runbook instance returns an empty result set in the right pane.

**Workaround**: None

### Identifiers are displayed instead of activity names on the Runbook Tester canvas and log view area

**Description**: : Identifiers are displayed instead of Activity Names on the Runbook Tester canvas and Log View area. The Activity name is included as a property in the Log View area.

**Workaround**: If needed, Runbook tester of UR1 can be used which is compatible with Orchestrator 2022 UR2.

### Text content doesn't show correctly in the Runbook Tester log view area

**Description**: Text content doesn't show correctly in the Runbook Tester log view area. Selecting the text will re-render it in the correct font that supports all scripts including GB18030-2022 character set.

**Workaround**: None

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
