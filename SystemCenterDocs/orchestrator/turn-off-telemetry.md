---
ms.assetid: 17e19c04-7712-456c-a5ed-59a1237d05f5
title: Manage telemetry settings in System Center Orchestrator
description: This article provides information about how to manage the telemetry settings in System Center Orchestrator
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  05/22/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology: orchestrator
---

# Manage telemetry settings in Orchestrator

This article provides information about how to manage the telemetry (Diagnostics and utility data) settings in System Center - Orchestrator.

By default, Orchestrator sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time.

## Turn on/off telemetry from console

1. In the Orchestration console > toolbar, click **Help**.

2. In the **Help** menu, click **Send diagnostic and usage data to Microsoft**.

  ![console telemetry option](./media/telemetry/telemetry-option-help-menu.png)

3. Select the  diagnostic and usage data sharing preference from the options displayed, and click  **OK**.

  ![console telemetry selection](./media/telemetry/telemetry-option-selection.png)

## Telemetry data collected

| Data related To | Data collected |
| --- | --- |
| **Installation and other configuration information** | DataBase name  <br /><br /> Database authentication yype|
| **Usage** | Number of Runbook designers <br /><br /> Number of folders <br /><br /> Number of variables <br /><br /> Number of schedules <br /><br /> Number of runbooks<br /><br /> Number of computer groups <br /><br /> 	Number of integration packs  <br /><br />  Average load per minute on runbook server <br /><br /> Names of integration packs <br /><br /> Activity name in use <br /><br /> Run script types |


## Next steps
[Work with runbooks in Orchestrator console](console-overview.md)
