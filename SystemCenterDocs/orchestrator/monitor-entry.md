---
title: Monitor Entry
description: The Monitor Entry activity invokes a runbook when new entries are generated and/or existing entries are modified in HP Service Manager.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 8fe4ab70-2443-4fc6-a076-9405fd3ea2cf
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Monitor Entry

The Monitor Entry activity invokes a runbook when new entries are generated and/or existing entries are modified in HP Service Manager.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Service Manager Activities](service-manager-activities.md).

## Monitor Entry required properties

| Element   | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Name   | The type of entry to be created.   | Change, Incident, ServiceDesk   | Yes   |
| Subtype   | The subtype of the entry.  | This is a dynamic property based on the configuration of the HP Service Manager server | Yes   |
| New entries   | If selected the runbook will be triggered when new entries are detected.   | True<br>False   | No   |
| Updated entries | If selected the runbook will be triggered when modified entries are detected. | True<br>False   | No   |

## Time synchronization

Time synchronization between the Runbook Server and the HP Service Manager system is important to the operation of the Monitor Entry object. For this reason, the Monitor Entry object attempts multiple methods to synchronize the times of the systems. The object will first try to use the Domain time. If the Runbook Server user doesn't have the permission to perform a **NET TIME** command on the HP Service Manager system, then the object will attempt to retrieve the information from the database. If the ODBC driver isn't present on the Runbook Server, then the object will default to use the local time of the Runbook Server. If you're experiencing problems with the Monitor Entry object, try one of the following:

- Ensure that the Runbook Server and the HP Service Manager are on the same domain and that the user assigned to the Runbook Server service is able to successfully perform a NET TIME command against the HP Service Manager system.
- Create an ODBC DSN on the Runbook Server that connects to the HP Service Manager database. Ensure that this DSN information is added to the connection information for that HP Service Manager system. For more information about creating connections to HP Service Manager, see [Configuring the HP Service Manager Connections](/previous-versions/system-center/packs/hh771464(v=technet.10)#ConfiguringConnections).
- Ensure that the locale and system times are synchronized between the Runbook Server and the HP Service Manager system.

## Other activities

The Integration Pack for HP Service Manager contains the following additional activities:

- [Close Entry](close-entry.md)
- [Create Entry](create-entry.md)
- [Get Entry](get-entry.md)
- [Update Entry](update-entry.md)
