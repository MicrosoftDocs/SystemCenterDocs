---
title: Download File
description: The Download File activity is used in a runbook to download a file from a FTP server.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1c357dc-b324-4bca-86be-b252c729b602
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Download File
=============

Applies To: System Center 2016 - Orchestrator

The Download File activity is used in a runbook to download a file from a FTP server.

This activity publishes all of the data from the required and optional properties into published data.

The following tables list the required and optional properties and published data for this activity.

Download File Required Properties
---------------------------------

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| File Mask   | The path and file mask of the file to download. The asterisk (\*) will match any number of characters. The question mark (?) will match any one character.   | String   |
| Local Path   | The local destination path where the files are copied.   | String   |
| Recursive   | Determines if folders contained in the subfolders will be copied if matching file mask.   | True<br>False   |
| Replace Existing Files (SFTP)   | Determines if existing files in the Local Path should be replaced. Only compatible with SFTP.   | True<br>False   |
| Representation Type   | Determines how data is transferred.   | Ascii<br>Binary   |
| ModeZ   | Enables Mode Z data decompression.   | True<br>False   |
| Error Action (FTP)   | Determines the action to take when an error occurs transferring files. Only compatible with FTP.<br>Abort - Activity should fail.<br>Ignore - Skip the file and continue with the next.<br>Retry - Attempt to retransfer the file. | Abort<br>Retry<br>Ignore |
| Recreate Folder Structure (FTP) | Determines if the directory structure should be recreated on the local machine. Only compatible with FTP.   | True<br>False   |

Download File Optional Properties
---------------------------------

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Retry Count (FTP) | The number of times to retry when Error Action is set to Retry. | Integer   |

Download File Published Data
----------------------------

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Count   | Number of files downloaded   | Integer   |
| Error Action (FTP)   | Action to take when an error occurs transferring files.   | Abort<br>Retry<br>Ignore   |
| File Mask   | The path and file mask of the file to download.   | String   |
| File Name   | The file name of each file downloaded.   | String   |
| File Path   | The file path for each file downloaded.   | String   |
| Local Path   | The local destination path where the files are copied.   | String   |
| ModeZ   | Mode Z data decompression.   | True<br>False   |
| Recreate Folder Structure (FTP) | Directory structure should be recreated on the local machine.   | True<br>False   |
| Recursive   | Folders contained in the subfolders will be copied if matching file mask. | True<br>False   |
| Replace Existing Files (SFTP)   | Existing files in the Local Path should be replaced.   | True<br>False   |
| Representation Type   | Data transfer type.   | Ascii<br>Binary   |
| Retry Count (FTP)   | The number of times to retry when Error Action is set to Retry.   | Integer   |
| Certificate Path (FTP)   | The file path for the certificate.   | String   |
| Connection Type   | The FTP connection type used to connect to the FTP server.   | Normal<br>ImplicitSslTls<br>NormalWithExplicitSsl30Authentication<br>NormalWithExplicitTlsSsl31Authentication<br>SFTP |
| HTTP Proxy Port (FTP)   | The port used to connect to the HTTP proxy server.   | Integer   |
| HTTP Proxy Server (FTP)   | The IP address or computer name of the HTTP proxy server.   | String   |
| HTTP Proxy Username (FTP)   | The user name used to connect to the HTTP proxy server.   | String   |
| Log   | Detailed FTP log.   | String   |
| Port   | The port used to connect to the FTP server.   | Integer   |
| Server   | The IP address or computer name of the FTP server.   | String   |
| Timeout   | The time to wait before a FTP operation times out.   | Integer   |
| Transfer Type (FTP)   | The transfer type used by FTP.   | Passive<br>Active   |
| Username   | The user name used to connect to the FTP server.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

