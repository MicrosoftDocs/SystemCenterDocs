---
title: Rename File or Folder
description: The Rename File/Folder activity is used in a runbook to rename a file or folder on an FTP server.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 1eeb6dcd-0579-4e33-b51d-db5241e6b0cc
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Rename File or Folder

The Rename File/Folder activity is used in a runbook to rename a file or folder on an FTP server.

This activity publishes all the data from the required properties into published data.

The following tables list the required properties and published data for this activity.

## Rename File/Folder required properties

| **Element** | **Description**   | **Valid Values** |
|:---|:---|:---|
| Path   | The relative or absolute path of the file or folder to rename. Absolute paths can be used provided the FTP server supports this feature. | String   |
| New Name   | The new name of the file or folder.   | String   |
| Type   | Determines the rename operation. Select Folder for renaming a folder. Select File for renaming a file.   | Folder<br>File   |

## Rename File/Folder published data

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| New Name   | The new name of the file or folder.   | String   |
| Path   | The relative or absolute path of the file or folder to rename. | String   |
| Previous Name   | The previous name of the file or folder.   | String   |
| Type   | The rename operation type   | Folder, File   |
| Certificate Path (FTP)   | The file path for the certificate.   | String   |
| Connection Type   | The FTP connection type used to connect to the FTP server.   | Normal<br>ImplicitSslTls<br>NormalWithExplicitSsl30Authentication<br>NormalWithExplicitTlsSsl31Authentication<br>SFTP |
| HTTP Proxy Port (FTP)   | The port used to connect to the HTTP proxy server.   | Integer   |
| HTTP Proxy Server (FTP)   | The IP address or computer name of the HTTP proxy server.   | String   |
| HTTP Proxy Username (FTP) | The user name used to connect to the HTTP proxy server.   | String   |
| Log   | Detailed FTP log.   | String   |
| Port   | The port used to connect to the FTP server.   | Integer   |
| Server   | The IP address or computer name of the FTP server.   | String   |
| Timeout   | The time to wait before an FTP operation times out.   | Integer   |
| Transfer Type (FTP)   | The transfer type used by FTP.   | Passive<br>Active   |
| Username   | The user name used to connect to the FTP server.   | String   |
