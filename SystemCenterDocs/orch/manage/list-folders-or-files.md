---
title: List Folders or Files
description: The List Folders/Files activity is used in a runbook to list the folders and files in the specified folder path.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7816e0c-c185-4f76-967d-5b501fe39f58
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# List Folders or Files

Applies To: System Center 2016 - Orchestrator

The List Folders/Files activity is used in a runbook to list the folders and files in the specified folder path.

This activity publishes all of the data from the required and optional properties into published data.

The following tables list the required and optional properties and published data for this activity.

## List Folders/Files Required Properties

| **Element**  | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Folder Path  | The path of the folder to list the contents of.   | String   |
| Recursive   | Determines if all contents of all nested children are returned. | True<br>False   |
| Filter Scope | Determines what items the list activity will return.   | All<br>File<br>Folder |

## List Folders/Files Optional Properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Date/Time (Max) | Last write date maximum filter. Must be used with Date/Time (Min). | Date Time   |
| Date/Time (Min) | Last write date minimum filter. Must be used with Date/Time (Max). | Date Time   |
| File Size (Max) | File size maximum filter. Must be used with File Size (Min).   | Integer   |
| File Size (Min) | File size minimum filter. Must be used with File Size (Max).   | Integer   |

## List Folders/Files Filters

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Archive Attribute   | The archive attribute of the folder or file.   | Equals   |
| Compressed Attribute   | The compressed attribute of the folder or file.   | Equals   |
| Device Attribute   | The device attribute of the folder or file.   | Equals   |
| Directory Attribute   | The directory attribute of the folder or file.   | Equals   |
| Encrypted Attribute   | The encrypted attribute of the folder or file.   | Equals   |
| Hidden Attribute   | The hidden attribute of the folder or file.   | Equals   |
| Name   | The name of the folder or file.   | Equals<br>Does not equal |
| Not Content Indexed Attribute | The content indexed attribute of the folder or file. | Equals   |
| Offline Attribute   | The offline attribute of the folder or file.   | Equals   |
| Read Only Attribute   | The read-only attribute of the folder or file.   | Equals   |
| Reparse Point Attribute   | The reparse point attribute of the folder or file.   | Equals   |
| SparseFile Attribute   | The sparsefile attribute of the folder or file.   | Equals   |
| System Attribute   | The system attribute of the folder or file.   | Equals   |
| Temporary Attribute   | The temporary attribute of the folder or file.   | Equals   |

## List Folders/Files Published Data

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Attributes   | File attributes for each item returned.   | String   |
| Has Attributes   | Has Attibutes for each item returned. Determines if the item has attributes that can be filtered. | Boolean   |
| Count   | Number of folders or files returned   | Integer   |
| Creation Date Time   | Creation date and time of item.   | Date Time   |
| Date/Time (Max)   | Last write date maximum filter.   | Date Time   |
| Date/Time (Min)   | Last write date minimum filter.   | Date Time   |
| File Name   | File name of each item returned.   | String   |
| File Size (Max)   | File size maximum filter.   | Integer   |
| File Size (Min)   | File size minimum filter.   | Integer   |
| Filter Scope   | Determines what items the list activity will return.   | All<br>File<br>Folder   |
| Full Name   | Full name of each item returned.   | String   |
| Hosted Full Name   | Hosted full name for each item returned.   | String   |
| Last Access Date Time   | Last access date time for each item returned.   | Date Time   |
| Last Write Date Time   | Last write date time for each item returned.   | Date Time   |
| Parent Folder   | Parent folder for each item returned.   | String   |
| Recursive   | All contents of all nested children are returned   | True<br>False   |
| Folder Path   | The path of the folder to list the contents of.   | String   |
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

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

