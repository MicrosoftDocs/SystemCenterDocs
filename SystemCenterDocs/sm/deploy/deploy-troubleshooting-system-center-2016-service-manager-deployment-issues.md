---
title: Troubleshooting System Center - Service Manager Deployment Issues
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4aee1627-a7c4-4299-847a-a5bfb87a4133
---

# Troubleshooting System Center 2016 - Service Manager Deployment Issues

>Applies To: System Center 2016 - Service Manager

An installation log file is captured during the installation of System Center 2016 – Service Manager. After Service Manager is running, various events are captured in the Windows Event Log. In addition, there are some Windows PowerShell commands that you can use to help troubleshoot data warehouse jobs. For more information, see [Troubleshoot Data Warehouse Jobs](../manage/admin-troubleshooting-a-data-warehouse-job.md).



## Installation Log Files

A log file, SCSMInstall.log, captures the progress of the installation. You can use this log file to troubleshoot a failed installation. You can find this log file in the %temp% folder. To troubleshoot installation problems, you can open the log files and search for a line that reads *Return Value 3*. If you find such a line in the log file, look above this line for any indication that a particular step failed.

## Event Logs

Service Manager event logs are located in Event Viewer, in the **Application and Service Logs/Microsoft/Operations Manager** folder.

## Create Database error

During setup, when you were configuring Service Manager or data warehouse databases, you were given the opportunity to specify how much disk space to allocate for each database. The default setting is 2,000 megabytes (MB) (2 gigabytes (GB)). In addition to the disk space that is required for the database, Service Manager sets aside additional space for file groups and log files. The additional space that is required for the file groups and log files can be equal to the space that is required for the database.

If there is insufficient disk space available, a message appears, indicating that an error occurred during execution of a custom action: `_CreateDatabase`. The installation stops before permanent changes are made. If you examine the Service Manager setup log, you find the following string:

```
Additional Error Description : MODIFY FILE encountered operating system error 112(There is not enough space on the disk.) while attempting to expand the physical file
```

You have to either increase the amount of free disk space that is available or reduce the amount of space that Service Manager allocates for the database, and then attempt the installation again. If you are installing Service Manager in a nonproduction environment, you can specify as little as 500 MB for the database.
