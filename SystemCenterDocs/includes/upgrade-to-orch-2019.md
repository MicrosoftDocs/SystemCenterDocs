---
ms.assetid: c5700b3d-d4a2-494c-9c37-de5bed7a0b5e
title:  include file  
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  09/07/2022
ms.topic:  include
ms.service:  system-center
ms.subservice: orchestrator
description: include file to provide an overview of how to upgrade your System Center Orchestrator installation to release 2019.
keywords:
ms.update-cycle: 1095-days
---

## Upgrade to System Center 2019 - Orchestrator

The following sections provide information about how to upgrade to System Center 2019 - Orchestrator.

>[!NOTE]
>  To upgrade to Orchestrator 2019 UR1 and later, ensure that [Microsoft OLE DB Driver for SQL Server](/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-2017#1860&preserve-view=true) is installed on machines that host the Management Server, Runbook Service, Runbook Designer, or the Web API Service. 

You can upgrade your installation of System Center 2016 Update Rollup (UR) 6, 1801 or 1807 Orchestrator to System Center 2019 Orchestrator by following the steps described below.

Before you attempt the upgrade, ensure that your environment is upgraded to the supported versions as described in [System Requirements for System Center 2019](../orchestrator/system-requirements-orch.md).

## Upgrade steps

**Prepare to upgrade:**

1. If you're using Orchestrator 2016, ensure you've UR6 installed.  
2. Ensure that there are no pending restarts on the computer.
3. Perform a full backup of Orchestrator database. For information about backing up the Orchestrator database, see [Migrate Orchestrator between environments](../orchestrator/migrate-orchestrator-between-environments.md).
4. Upgrade the hardware, operating system, and other software if necessary to meet the requirements of Orchestrator in System Center 2019.

**Perform the upgrade:**

1. Stop all Orchestrator runbooks.
2. Uninstall the Orchestrator management server, any runbook servers, the Web Service, and the Runbook Designer.
3. Install the Orchestrator management server in System Center 2019, as described in [Install Orchestrator](../orchestrator/install.md).
4. Install any Orchestrator Runbook servers in System Center 2019.
5. Install the Orchestrator Runbook Designer in System Center 2019.
6. If needed, install the Orchestrator Web Service in System Center 2019.
