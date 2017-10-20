---
title: Synchronize Folder or File
description: The Synchronize Folder/File activity is used in a runbook to perform a one way synchronization of a folder/File.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ebe29f05-8025-4ad0-a77f-0171289e20a7
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Synchronize Folder or File

Applies To: System Center 2016 - Orchestrator

The Synchronize Folder/File activity is used in a runbook to perform a one way synchronization of a folder/File.

This activity publishes all of the data from the required and optional properties into published data.

The following tables list the required and optional properties and published data for this activity.

## Synchronize Folder/File Required Properties

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Remote Folder | The remote folder   | String   |
| Local Folder  | The local folder   | String   |
| Master Folder | Determines which folder is the master.   | Remote<br>Local   |
| Filter Scope  | Determines the scope of selected filters. | All<br>File<br>Folder |

## Synchronize Folder/File Optional Properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Allow Deletions   | Determines if deletions will be allowed during synchronization.   | True<br>False   |
| Auto Conflict Resolution | Determines if conflicts are automatically resolved. If False, synchronization will stop. | True<br>False   |
| Date/Time (Max)   | Last write date maximum filter. Must be used with Date/Time (Min).   | Date Time   |
| Date/Time (Min)   | Last write date minimum filter. Must be used with Date/Time (Max).   | Date Time   |
| File Size (Max)   | File size maximum filter. Must be used with File Size (Min).   | Integer   |
| File Size (Min)   | File size minimum filter. Must be used with File Size (Max).   | Integer   |
| Synchronize Sub-folders  | Determines if sub-folders will be synchronized.   | True<br>False   |

## Synchronize Folder/File Filters

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Archive Attribute   | The archive attribute of the folder or file.   | Equals   |
| Compressed Attribute   | The compressed attribute of the folder or file.   | Equals   |
| Device Attribute   | The device attribute of the folder or file.   | Equals   |
| Directory Attribute   | The directory attribute of the folder or file.   | Equals   |
| Encrypted Attribute   | The encrypted attribute of the folder or file.   | Equals   |
| Hidden Attribute   | The hidden attribute of the folder or file.   | Equals   |
| Name   | The name of the folder or file .   | Equals<br>Does not equal |
| Not Content Indexed Attribute | The content indexed attribute of the folder or file. | Equals   |
| Offline Attribute   | The offline attribute of the folder or file.   | Equals   |
| Read Only Attribute   | The read-only attribute of the folder or file.   | Equals   |
| Reparse Point Attribute   | The reparse point attribute of the folder or file.   | Equals   |
| SparseFile Attribute   | The sparsefile attribute of the folder or file.   | Equals   |
| System Attribute   | The system attribute of the folder or file.   | Equals   |
| Temporary Attribute   | The temporary attribute of the folder or file.   | Equals   |

## Synchronize Folder/File Published Data

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Allow Deletions   | Deletions will be allowed during synchronization.   | True<br>False   |
| Auto Conflict Resolution  | Conflicts are automatically resolved.   | True<br>False   |
| Count   | Number of files synchronized.   | Integer   |
| Date/Time (Max)   | Last write date maximum filter.   | Date Time   |
| Date/Time (Min)   | Last write date minimum filter.   | Date Time   |
| File Name   | File name of each file synchronized.   | String   |
| File Path   | File path for each file synchronized   | String   |
| File Size (Max)   | File size maximum filter.   | Integer   |
| File Size (Min)   | File size minimum filter.   | Integer   |
| Filter Scope   | Determines the scope of selected filters.   | All<br>File<br>Folder   |
| Local Folder   | The local folder.   | String   |
| Master Folder   | Which folder is the master.   | Remote, Local   |
| Remote Folder   | The remote folder.   | String   |
| Synchronize Sub-folders   | Sub-folders will be synchronized.   | True, False   |
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

## Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

