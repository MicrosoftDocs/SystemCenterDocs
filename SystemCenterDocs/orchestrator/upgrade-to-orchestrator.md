---
title:  Upgrade to System Center - Orchestra
description:  Upgrade instructions for System Center - Orchestra
author: rayne-wiselman
manager:  carmonm
ms.date:  01/17/2018
ms.prod:  system-center-threshold
ms.technology:  system-center-2016
ms.topic:  article
ms.author: raynew
monikerRange: 'sc-orch-2016'
---



# Upgrade in Orchestrator

You can upgrade to System Center 2016 - Orchestrator using the steps below.


## Before you start

- Make sure your environment has the latest supported versions described in [system requirements](system-requirements.md).
- To upgrade a server running Orchestra 2012 R2 to 2016, the server must be running System Center 2012 R2 rollup 8 or later.
- [Learn more](/system-center/upgrade-to-system-center-2016) about upgrading System Center components.

## Upgrade steps

**Prepare to upgrade:**

1. Ensure that there are no pending restarts on the computer.
2. Perform a full back up  of Orchestrator database. For information about backing up the Orchestrator database, see [Migrate Orchestrator between environments](migrate-orchestrator-between-environments.md).
3. Upgrade the hardware, operating system, and other software if needed.

**Perform the upgrade:**

1. Stop all Orchestrator runbooks.
2. Uninstall the Orchestrator management server, any runbook servers, the Web Service, and the Runbook Designer.
3. Install the new version of the Orchestrator management server. [Learn more](install.md).
4. Install the new version of any Orchestrator runbook servers.
5. Install the new version of the Orchestrator Runbook Designer.
6. If needed, install the Orchestrator Web Service.

## Next Steps

[Learn how](deploy-runbooks.md) to deploy runbooks
