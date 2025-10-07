---
title:  TCP port requirements in System Center Orchestrator
description: This article describes the port requirements for System Center Orchestrator.
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: orchestrator
ms.assetid: 6e89c2ee-583a-41df-a94c-47f349f954ef
monikerRange: 'sc-orch-2016 || sc-orch-2019 || sc-orch-2022'
---
# TCP port requirements

Communication between Orchestrator features on different computers occurs over TCP/IP. If you've firewalls in your environment between these features, you must enable the ports indicated in the following table:

| Source  | Targeted computer| Default port | Configurable | Notes |
|-------|--------|-------|----|------|
| Runbook Designer  | Management server   | 135, 1024-65535  | Yes      | The Runbook Designer communicates with the management server over DCOM. By default, DCOM communicates over port 135 and dynamically allocates a port between 1024 and 65535. For information about configuring DCOM for a specific port range, see [Configuring Microsoft Distributed Transaction Coordinator (DTC) to work through a firewall](/troubleshoot/windows-server/application-management/configure-dtc-to-work-through-firewalls). |
| Management server   <br> <br> runbook server <br><br> Web service      |  orchestration database   | 1433    | Yes  | Specified during Microsoft SQL Server installation |
| Client browser | Orchestrator REST-based web service  | 81  | Yes   | Specified during Orchestrator installation. Both Port 81 and Port 82 must be accessible for the Orchestration console.      |
| Client browser     | Orchestration console   | 82  | Yes   | Specified during Orchestrator installation. Both Port 81 and Port 82 must be accessible for the Orchestration console.          |
| Activities   | Various targeted computers depending on activity | |   | For information about individual integration packs, see [Integration Packs for System Center - Orchestrator](list-of-orchestrator-integration-packs.md).    |

### Next steps
- [See system requirements](system-requirements-orch.md).
- [Install Orchestrator](install.md).
