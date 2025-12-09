---
ms.assetid:
description: include file to summarize the release notes for System Center 2022 - Orchestrator
ms.topic:  include
author: Jeronika-MS
ms.author: v-gajeronika
ms.service:  system-center
ms.subservice: Orchestrator
keywords:
ms.date: 12/09/2025
title:  include file
---

## Orchestrator 2022 UR3 GB issues hotfix Release notes

The following sections summarize the release notes for Orchestrator 2022 UR3 GB issues hotfix, and include the known issues and workarounds.

For the problems fixed in UR3 GB issues hotfix and the installation instructions for UR3 GB issue hotfix, see the [KB article](https://support.microsoft.com/kb/5072592).

- Conform GB18030-2022 Amendment standard. 

The following sections summarize the known issues and workarounds in System Center Orchestrator 2022 UR3 hotfix:

### Upgrade from Orchestrator 2019 to Orchestrator 2022 might have Web Console errors due to time out issue

**Workaround**: For better web console performance, [download the SQL script](https://download.microsoft.com/download/9/f/b/9fba34ab-dee3-4735-8771-dc7c7c5da341/SCO22_UR2_SP_Update%201.sql), open SQL Server Management Studio, connect to your Orchestrator database, and execute the script.

## Orchestrator 2022 UR3 Release notes

The following sections summarize the release notes for Orchestrator 2022 UR3, and include the known issues and workarounds.

For the problems fixed in UR3 and the installation instructions for UR3, see the [KB article](https://support.microsoft.com/topic/update-rollup-3-for-system-center-2022-orchestrator-aef5d811-c845-47c0-abc2-82ea9e74994a).

### Text content does not show correctly in the Runbook Tester log view area

**Description**: Text content does not show correctly in the Runbook Tester log view area. Selecting the text will re-render it in the correct font that supports all scripts including GB18030-2022 character set.

**Workaround**: None

### Service Manager connector doesn't work with new Web API

**Description**: Service Manager (SM) console doesn't detect Orchestrator 2022 installation because the Connector for the new Web API is yet to be released.

**Workaround**: Install the Orchestrator 2019 Web features on the computer alongside Orchestrator 2022. Ensure to configure the Orchestrator 2022 database in the 2019 Web features. The SM connector can monitor Orchestrator 2022 with Orchestrator 2019 Web service.

## Orchestrator 2022 UR2 release notes

The following sections summarize the release notes for Orchestrator 2022 UR2, and include the known issues and workarounds.

For the problems fixed in UR2 and the installation instructions for UR2, see [the KB article](https://support.microsoft.com/kb/5033099).

### 'Send platform event' activity isn't persisted to the database

**Description**: **Send platform event** activity isn't persisted to the database and isn't visible in **Events** tab of the Runbook Designer.

**Workaround**: None

### Identifiers are displayed instead of activity names on the Runbook Tester canvas and log view area

**Description**: Identifiers are displayed instead of Activity Names on the Runbook Tester canvas and Log View area. The Activity name is included as a property in the Log View area.

**Workaround**: If needed, Runbook tester of UR1 can be used, it is compatible with SCO UR2.

### Text content does not show correctly in the Runbook Tester log view area

**Description**: Text content does not show correctly in the Runbook Tester log view area. Selecting the text will re-render it in the correct font that supports all scripts including GB18030-2022 character set.

**Workaround**: None

### Service Manager connector doesn't work with new Web API

**Description**: Service Manager (SM) console doesn't detect Orchestrator 2022 installation because the Connector for the new Web API is yet to be released.

**Workaround**: Install the Orchestrator 2019 Web features on the computer alongside Orchestrator 2022. Ensure to configure the Orchestrator 2022 database in the 2019 Web features. The SM connector can monitor Orchestrator 2022 with Orchestrator 2019 Web service.

### Runbook designer crashes with some Integration packs

**Description**: With some integration packs, Runbook designer might crash when you update existing runbooks or create new runbooks.

**Mitigation**: Install the [Hotfix](https://www.catalog.update.microsoft.com/Search.aspx?q=5033783) for Orchestrator 2022 UR2 that fixes this issue.

## Orchestrator 2022 UR1 release notes

The following sections summarize the release notes for Orchestrator 2022 UR1, and include the known issues and workarounds.

For the problems fixed in UR1 and the installation instructions for UR2, see [the KB article](https://support.microsoft.com/kb/5021420).

### 'Send platform event' activity isn't persisted to the database

**Description**: **Send platform event** activity isn't persisted to the database and isn't visible in **Events** tab of the Runbook Designer.

**Workaround**: None

### Issues with Exchange Admin Integration pack v10.22.1.x

**Description**: Issues with Exchange Admin Integration pack v10.22.1.x

**Workaround**: Upgrade to SCO 2022 Exchange Admin Integration pack version 10.22.2.5 or later. For more details, refer [blog announcement](https://techcommunity.microsoft.com/t5/system-center-blog/update-sc-orchestrator-exchange-admin-2022-integration-pack-v10/ba-p/3828422).


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

## Orchestrator 2022 release notes

The Orchestrator 2022 release includes all issues fixed until [Orchestrator 2019 UR3](https://support.microsoft.com/topic/update-rollup-3-for-system-center-2019-orchestrator-70bc1df6-adbc-9b89-68bf-df5a6eefca5f).

>[!NOTE]
>System Center Orchestrator 2019 IPs aren't supported on System Center Orchestrator 2022. 
