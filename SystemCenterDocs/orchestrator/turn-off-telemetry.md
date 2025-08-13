---
ms.assetid: 17e19c04-7712-456c-a5ed-59a1237d05f5
title: Manage telemetry settings in System Center Orchestrator
description: This article provides information about how to manage the telemetry settings in System Center Orchestrator
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: orchestrator
ms.custom: UpdateFrequency2
---

# Manage telemetry settings in Orchestrator

This article provides information about how to manage the telemetry (Diagnostics and utility data) settings in System Center - Orchestrator.

By default, Orchestrator sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security, and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time.

## Turn on/off telemetry from console

1. In the Orchestration console > toolbar, select **Help**.

2. In the **Help** menu, select **Send diagnostic and usage data to Microsoft**.

   ![Screenshot of console telemetry option.](./media/telemetry/telemetry-option-help-menu.png)

3. Select the  diagnostic and usage data sharing preference from the options displayed, and select **OK**.

   ![Screenshot of console telemetry selection.](./media/telemetry/telemetry-option-selection.png)

   >[!NOTE]
   >We recommend that you read the Privacy Statement before you select the option.

   -  To turn on telemetry, select **Yes, I am willing to send data to Microsoft**.
   - 	To turn off telemetry, select **No, I prefer not to send data to Microsoft**.

## Telemetry data collected

| Data related To | Data collected |
| --- | --- |
| **Installation and other configuration information** | DataBase name  <br /><br /> Database authentication type|
| **Usage** | Number of Runbook designers <br /><br /> Number of folders <br /><br /> Number of variables <br /><br /> Number of schedules <br /><br /> Number of runbooks<br /><br /> Number of computer groups <br /><br /> 	Number of integration packs  <br /><br />  Average load per minute on runbook server <br /><br /> Names of integration packs <br /><br /> Activity name in use <br /><br /> Run script types |

## Next steps

[Work with runbooks in Orchestrator console](console-overview.md).
