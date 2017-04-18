---
title:  Upgrade to Orchestrator-2016
author:  cfreemanwa
ms.author: cfreeman
manager:  cfreeman
ms.date:  10/12/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  system-center-2016
ms.assetid: 48eb18c8-ef09-4f5f-b846-0be2aea84f33
description: This article provides an overview of how to upgrade your System Center Orchestrator installation.
keywords:
---

# Upgrade to Orchestrator 2016

>Applies To: System Center 2016 - Orchestrator

You can upgrade your installation of System Center 2012 R2 - Orchestrator to System Center 2016 Orchestrator by following the steps described below. Before doing so, make sure your environment is upgraded to the supported versions as described in [System Requirements for System Center 2016](system-requirements.md).

>[!Note]
>Upgrading from System Center 2012 R2 - Orchestrator is only supported if you have installed Upgrade Rollup 8 or later.

## Orchestrator upgrade steps

**Prepare to upgrade:**

1. Ensure that there are no pending restarts on the computer.
2. Perform a full back up  of Orchestrator database. For information about backing up the Orchestrator database, see [Migrate Orchestrator between environments](migrate-orchestrator-between-environments.md).
3. Upgrade the hardware, operating system, and other software if necessary to meet the requirements of Orchestrator in System Center 2016.

**Perform the upgrade:**

1. Stop all Orchestrator runbooks.
2. Uninstall the Orchestrator management server, any runbook servers, the Web Service, and the Runbook Designer.
3. Install the Orchestrator management server in System Center 2016, as described in [Install Orchestrator](../orch/deploy/install-orchestrator.md).
4. Install any Orchestrator runbook servers in System Center 2016.
5. Install the Orchestrator Runbook Designer in System Center 2016.
6. If needed, install the Orchestrator Web Service in System Center 2016.
