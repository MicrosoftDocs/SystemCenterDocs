---
ms.assetid: ba25182b-5ddf-439e-8dd6-541194e65168
title:  include file  
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  05/17/2018
ms.topic:  include
ms.service:  system-center
ms.subservice: orchestrator
description: include file to provide an overview of how to upgrade your System Center Orchestrator installation to release 1801.
keywords:
---

## Upgrade to System Center 1801 - Orchestrator

The following sections provide information about how to upgrade to System Center 1801 - Orchestrator.

You can upgrade your installation of System Center 2012 R2 Update Rollup (UR) 14 and 2016 UR4 Orchestrator to System Center 1801 Orchestrator by following the steps described below. Before doing so, ensure that your environment is upgraded to the supported versions as described in [System Requirements for System Center 1801](../orchestrator/system-requirements-orch.md).

## Upgrade steps

**Prepare to upgrade:**

1. For 2012 R2, ensure you've UR14 installed, and for 2016, UR4 installed.  
2. Ensure that there are no pending restarts on the computer.
3. Perform a full backup of Orchestrator database. For information about backing up the Orchestrator database, see [Migrate Orchestrator between environments](../orchestrator/migrate-orchestrator-between-environments.md).
4. Upgrade the hardware, operating system, and other software if necessary to meet the requirements of Orchestrator in System Center 1801.

**Perform the upgrade:**

1. Stop all Orchestrator runbooks.
2. Uninstall the Orchestrator management server, any runbook servers, the Web Service, and the Runbook Designer.
3. Install the Orchestrator management server in System Center 1801, as described in [Install Orchestrator](../orchestrator/install.md).
4. Install any Orchestrator Runbook servers in System Center 1801.
5. Install the Orchestrator Runbook Designer in System Center 1801.
6. If needed, install the Orchestrator Web Service in System Center 1801.
