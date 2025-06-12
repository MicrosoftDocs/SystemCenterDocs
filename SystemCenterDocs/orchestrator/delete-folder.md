---
title: Delete Folder
description: The Delete Folder activity is used in a runbook to delete a folder on an FTP server.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2692378a-ba5e-4e1f-ac74-8019d17e6e24
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---
# Delete folder on an FTP server

The Delete Folder activity is used in a runbook to delete a folder on an FTP server.

This activity publishes all the data from the required properties into published data.

The following tables list the required properties and published data for this activity.

## Delete Folder Required Properties

| **Element** | **Description**   | **Valid Values** |
|:---|:---|:---|
| Folder Path | The relative or absolute path of the folder to delete. Absolute paths can be used provided the FTP server supports this feature. The asterisk (\*) and question mark (?) aren't supported. | String   |

## Deleted Folder Published Data

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Folder Path   | The path of the folder to delete.   | String   |
| Item Path   | The file or folder path of each item deleted inside the folder. | String   |
| Count   | The number of items deleted.   | Integer   |
| Certificate Path (FTP)   | The file path for the certificate.   | String   |
| Connection Type   | The FTP connection type used to connect to the FTP server.   | Normal<br>ImplicitSslTls<br>NormalWithExplicitSsl30Authentication<br>NormalWithExplicitTlsSsl31Authentication<br>SFTP |
| HTTP Proxy Port (FTP)   | The port used to connect to the HTTP proxy server.   | Integer   |
| HTTP Proxy Server (FTP)   | The IP address or computer name of the HTTP proxy server.   | String   |
| HTTP Proxy Username (FTP) | The user name used to connect to the HTTP proxy server.   | String   |
| Log   | Detailed FTP log.   | String   |
| Port   | The port used to connect to the FTP server.   | Integer   |
| Server   | The IP address or computer name of the FTP server.   | String   |
| Timeout   | The time to wait before an FTP operation times out.   | Integer   |
| Transfer Type (FTP)   | The transfer type used by FTP.   | Passive,<br>Active   |
| Username   | The user name used to connect to the FTP server.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
