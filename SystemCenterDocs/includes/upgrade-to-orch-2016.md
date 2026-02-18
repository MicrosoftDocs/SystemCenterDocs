---
ms.assetid: 7b623b69-e0f1-4461-aa45-6d9a2e965cfd
title:  include file
description:  include file to provide the upgrade instructions for System Center 2016 - Orchestrator
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  o5/17/2018
ms.service:  system-center
ms.subservice:  orchestrator
ms.topic:  include
ms.update-cycle: 1095-days
---


## Upgrade to System Center 2016 - Orchestrator

The following sections provide information about how to upgrade to System Center 2016 - Orchestrator.


## Before you start

- Ensure that your environment has the latest supported versions described in [system requirements](../orchestrator/system-requirements-orch.md).
- To upgrade a server running Orchestrator 2012 R2 to 2016, the server must be running System Center 2012 R2 rollup 8 or later.
- [Learn more](../upgrade-to-system-center-2016.md) about upgrading System Center components.

## Upgrade steps

**Prepare to upgrade:**

1. Ensure that there are no pending restarts on the computer.
2. Perform a full backup of Orchestrator database. For information about backing up the Orchestrator database, see [Migrate Orchestrator between environments](../orchestrator/migrate-orchestrator-between-environments.md).
3. Upgrade the hardware, operating system, and other software if needed.

**Perform the upgrade:**

1. Stop all Orchestrator runbooks.
2. Uninstall the Orchestrator management server, any runbook servers, the Web Service, and the Runbook Designer.
3. Install the new version of the Orchestrator management server. [Learn more](../orchestrator/install.md).
4. Install the new version of any Orchestrator runbook servers.
5. Install the new version of the Orchestrator Runbook Designer.
6. If needed, install the Orchestrator Web Service.