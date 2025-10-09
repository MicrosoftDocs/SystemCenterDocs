---
title: Create Folder
description: The Create Folder activity is used in a runbook to create a folder on an FTP server.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: b57dd2f6-55d8-4a08-97de-4be6efc8d612
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Create Folder

The Create Folder activity is used in a runbook to create a folder on an FTP server.

This activity publishes all of the data from the required properties into published data.

The following tables list the required properties and published data for this activity.

## Create Folder Required Properties

| **Element** | **Description**   | **Valid Values** |
|:---|:---|:---|
| Folder Path | The relative or absolute path of the folder to create. Absolute paths can be used provided the FTP server supports this feature. | String   |

## Create Folder Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Folder Name   | The name of the folder.   | String   |
| Folder Path   | The complete path of the created folder.   | String   |
| Certificate Path (FTP)   | The file path for the certificate.   | String   |
| Connection Type   | The FTP connection type used to connect to the FTP server. | String   |
| HTTP Proxy Port (FTP)   | The port used to connect to the HTTP proxy server.   | Integer   |
| HTTP Proxy Server (FTP)   | The IP address or computer name of the HTTP proxy server.  | String   |
| HTTP Proxy Username (FTP) | The user name used to connect to the HTTP proxy server.   | String   |
| Log   | Detailed FTP log.   | String   |
| Port   | The port used to connect to the FTP server.   | Integer   |
| Server   | The IP address or computer name of the FTP server.   | String   |
| Timeout   | The time to wait before an FTP operation times out.   | Integer   |
| Transfer Type (FTP)   | The transfer type used by FTP.   | String   |
| Username   | The user name used to connect to the FTP server.   | String   |

#### Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
