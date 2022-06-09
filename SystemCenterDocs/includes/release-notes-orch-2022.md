---
ms.assetid:
description: include file to summarize the release notes for System Center 2022 - Orchestrator
manager: evansma
ms.topic:  include
author: jyothisuri
ms.author: jsuri
ms.prod:  system-center
ms.technology: Orchestrator
keywords:
ms.date: 03/21/2022
title:  include file
---

##  Orchestrator 2022 release notes

The Orchestrator 2022 release includes all issues fixed till [Orchestrator 2019 UR3](https://support.microsoft.com/topic/update-rollup-3-for-system-center-2019-orchestrator-70bc1df6-adbc-9b89-68bf-df5a6eefca5f).

>[!NOTE]
>- System Center Orchestrator 2022 Integration Packs are yet to be released.
>- System Center Orchestrator 2019 IPs are not supported on System Center Orchestrator 2022. 
>- If you are dependent on Microsoft released IPs, do not upgrade to ORCH 2022, until the IPs are released.

The following are the known issues and workarounds in System Center 2022 - Orchestrator.

## Known Issues and Workarounds

### Orchestrator Web console is not compatible with Internet Explorer

**Work around**: Open the Orchestrator web console with Microsoft Edge or other modern browsers. The new console does not depend on Silverlight.

### Orchestration Console navigation pane does not render properly when deeply nested

**Description**:Deeply nested Runbooks don't render correctly because the text overflows the width of the pane.

**Workaround**: None

### Runbooks that are not inside any folder (root runbooks) are not shown on the navigation pane

**Workaround**: Move root runbooks to a folder

### Job form requires output parameter also

**Workaround**: Use any string as value, it will be overwritten by the runbook execution with the output.


### Orchestrator Remoting Service and Runbook Server Monitor Service don’t exit cleanly

**Description**: The *oremoting* and *omonitor* service cannot be stopped using Service kill.

**Work around**: Kill the service process manually using Task Manager or by using the following command:

```cmd

taskkill /f /pid {pid of the service}

```
### Service Manager connector does not work with new Web API

**Description**: Service Manager (SM) console does not detect orchestrator 2022 installation, because the Connector for the new Web API is yet to be released.

**Workaround**: Install the Orchestrator 2019 Web features on the computer alongside Orchestrator 2022. Ensure to configure the Orchestrator 2022 database in the 2019 Web features. The SM connector can monitor Orchestrator 2022 with Orchestrator 2019 Web service.
