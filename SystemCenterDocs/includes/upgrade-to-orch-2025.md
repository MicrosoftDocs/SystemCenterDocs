---
ms.assetid: c5700b3d-d4a2-494c-9c37-de5bed7a0b5e
title:  include file  
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date:  03/18/2025
ms.topic:  include
ms.service:  system-center
ms.subservice: orchestrator
description: include file to provide an overview of how to upgrade your System Center Orchestrator installation to release 2025.
keywords:
---

## Upgrade to System Center 2025 - Orchestrator

The following sections provide information about how to upgrade to System Center 2025 - Orchestrator.

You can upgrade your installation of System Center 2022 Orchestrator to System Center 2025 Orchestrator by using the information in the below sections:

>[!NOTE]
>- To upgrade to Orchestrator 2025, ensure that [Microsoft OLE DB Driver v19 for SQL Server](https://learn.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server?view=sql-server-ver16&preserve-view=true) is installed on machines that host the Management Server, Runbook Service, Runbook Designer, or the Web API Service.
>- Connection to SQL is encrypted by default. To establish connection, install Trusted Server Certificate or follow steps mentioned  in [Secure Connection to SQL server](/system-center/orchestrator/install?view=sc-orch-2025#secure-connection-to-sql-server).
>- Before you attempt the upgrade, ensure that your environment is upgraded to the supported versions as described in [System Requirements for System Center 2025](../orchestrator/system-requirements-orch.md).

## Upgrade steps

**Prepare to upgrade:**

1. It's recommended to have the latest Update Rollup installed on Orchestrator 2022.
2. Ensure that there are no pending restarts on the computer.
3. Perform a full backup of Orchestrator database. For information about backing up the Orchestrator database, see [Migrate Orchestrator between environments](../orchestrator/migrate-orchestrator-between-environments.md).
4. Upgrade the hardware, operating system, and other software if necessary to meet the requirements of Orchestrator in System Center 2025.

**Perform the upgrade:**

1. Stop all Orchestrator runbooks.
2. Uninstall the Orchestrator management server, any runbook servers, the Web components, and the Runbook Designer.
3. Install the Orchestrator management server in System Center 2025 as described in [Install Orchestrator](../orchestrator/install.md).
4. Install any Orchestrator Runbook servers in System Center 2025.
5. Install the Orchestrator Runbook Designer in System Center 2025.
6. If needed, install the Orchestrator Web components in System Center 2025.
