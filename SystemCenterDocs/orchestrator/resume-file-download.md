---
title: Resume File Download
description: The Resume File Download activity is used in a runbook to resume a file download.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 99aa7184-cdd0-467a-9624-9d75821e38d2
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Resume File Download

> Applies To: System Center 2016 - Orchestrator

The Resume File Download activity is used in a runbook to resume a file download. This activity is only compatible with an FTP configuration.

This activity publishes all of the data from the required properties into published data.

The following tables list the required properties and published data for this activity.

## Resume File Download required properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Remote File Path   | The path of the remote file.   | String   |
| Local File Path   | The local path of the file to resume downloading. | String   |
| Representation Type | Determines how data is transferred.   | Ascii<br>Binary  |
| ModeZ   | Enables Mode Z data decompression.   | True<br>False   |

## Resume File Download published data

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Local File Path   | The local path of the file to resume downloading.   | String   |
| ModeZ   | Mode Z data decompression.   | True<br>False   |
| Remote File Path   | The path of the remote file.   | String   |
| Representation Type   | Data transfer type.   | Ascii<br>Binary   |
| Certificate Path (FTP)   | The file path for the certificate.   | String   |
| Connection Type   | The FTP connection type used to connect to the FTP server. | Normal<br>ImplicitSslTls<br>NormalWithExplicitSsl30Authentication<br>NormalWithExplicitTlsSsl31Authentication<br>SFTP |
| HTTP Proxy Port (FTP)   | The port used to connect to the HTTP proxy server.   | Integer   |
| HTTP Proxy Server (FTP)   | The IP address or computer name of the HTTP proxy server.  | String   |
| HTTP Proxy Username (FTP) | The user name used to connect to the HTTP proxy server.   | String   |
| Log   | Detailed FTP log.   | String   |
| Port   | The port used to connect to the FTP server.   | Integer   |
| Server   | The IP address or computer name of the FTP server.   | String   |
| Timeout   | The time to wait before a FTP operation times out.   | Integer   |
| Transfer Type (FTP)   | The transfer type used by FTP.   | Passive<br>Active   |
| Username   | The user name used to connect to the FTP server.   | String   |
