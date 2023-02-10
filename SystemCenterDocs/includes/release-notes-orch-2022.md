---
ms.assetid:
description: include file to summarize the release notes for System Center 2022 - Orchestrator
manager: mkluck
ms.topic:  include
author: jyothisuri
ms.author: jsuri
ms.prod:  system-center
ms.technology: Orchestrator
keywords:
ms.date: 03/21/2022
title:  include file
---

## Orchestrator 2022 release notes

The Orchestrator 2022 release includes all issues fixed until [Orchestrator 2019 UR3](https://support.microsoft.com/topic/update-rollup-3-for-system-center-2019-orchestrator-70bc1df6-adbc-9b89-68bf-df5a6eefca5f).

>[!NOTE]
>System Center Orchestrator 2019 IPs aren't supported on System Center Orchestrator 2022. 

### Update Rollup 1 (12 January 2023)

See [KB article #5021420](https://support.microsoft.com/kb/5021420) for improvements and issues fixed in 2022 UR1.

## Known Issues and Workarounds

The following are the known issues and workarounds in System Center 2022 - Orchestrator.

### Orchestrator Web console doesn't work properly

**Description**: Web Console doesn't work properly if .NET Core 5 isn't installed.

**Workaround**: Install .NET Core 5.

### Orchestrator Web console isn't compatible with Internet Explorer

**Workaround**: Open the Orchestrator web console with Microsoft Edge or other modern browsers. The new console doesn't depend on Silverlight.

### Orchestration Console navigation pane doesn't render properly when deeply nested

**Description**: Deeply nested Runbooks don't render correctly because the text overflows the width of the pane.

**Workaround**: None

### Runbooks that aren't inside any folder (root runbooks) aren't shown on the navigation pane

**Workaround**: Move root runbooks to a folder.

### Job form requires output parameter also

**Workaround**: Use any string as value, it will be overwritten by the runbook execution with the output.

### Orchestrator Remoting Service and Runbook Server Monitor Service don’t exit cleanly

**Description**: The *oremoting* and *omonitor* services can't be stopped using Service kill.

**Workaround**: Kill the service process manually using Task Manager or by using the following command:

```cmd

taskkill /f /pid {pid of the service}

```

### Service Manager connector doesn't work with new Web API

**Description**: Service Manager (SM) console doesn't detect Orchestrator 2022 installation because the Connector for the new Web API is yet to be released.

**Workaround**: Install the Orchestrator 2019 Web features on the computer alongside Orchestrator 2022. Ensure to configure the Orchestrator 2022 database in the 2019 Web features. The SM connector can monitor Orchestrator 2022 with Orchestrator 2019 Web service.
