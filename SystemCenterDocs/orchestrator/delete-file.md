---
title: Delete File
description: The Delete File activity is used in a runbook to delete a file on a FTP server.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a7fe1669-71b4-4f8b-a3c2-7b5c032dae91
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Delete File

The Delete File activity is used in a runbook to delete a file on a FTP server.

This activity publishes all of the data from the required properties into published data.

The following tables list the required properties and published data for this activity.

## Delete File Required Properties

| **Element** | **Description**   | **Valid Values** |
|:---|:---|:---|
| File Path   | The path of the file to delete. The asterisk (\*) will match any number of characters. The question mark (?) will match any one character. | String   |

## Delete File Published Data

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Count   | The number of files deleted.   | Integer   |
| Deleted File   | The file path for each file deleted.   | String   |
| File Path   | The path of the file to delete.   | String   |
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

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
