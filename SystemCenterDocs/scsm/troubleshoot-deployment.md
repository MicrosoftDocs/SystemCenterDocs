---
title: Troubleshoot System Center - Service Manager deployment issues
description: Describes how to troubleshoot System Center - Service Manager deployment issues.
ms.service: system-center
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 03/04/2025
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.custom: UpdateFrequency2, engagement-fy24
---

# Troubleshoot Service Manager deployment issues

This article describes how to troubleshoot System Center - Service Manager deployment issues.

An installation log file is captured during the installation of System Center – Service Manager. After Service Manager is running, various events are captured in the Windows Event Log. In addition, there are some Windows PowerShell commands that you can use to help troubleshoot data warehouse jobs. For more information, see [Troubleshoot data warehouse jobs](manage-dw.md).

## Installation log files

A log file, SCSMInstall.log, captures the progress of the installation. You can use this log file to troubleshoot a failed installation. You can find this log file in the %temp% folder. To troubleshoot installation problems, you can open the log files and search for a line that reads *Return Value 3*. If you find such a line in the log file, look above this line for any indication that a particular step failed.

## Event logs

Service Manager event logs are located in Event Viewer in the **Application and Service Logs/Microsoft/Operations Manager** folder.

## Create database error

During setup, when you were configuring Service Manager or data warehouse databases, you were given the opportunity to specify how much disk space to allocate for each database. The default setting is 2,000 megabytes (MB) (2 gigabytes (GB)). In addition to the disk space that is required for the database, Service Manager sets aside additional space for file groups and log files. The additional space that is required for the file groups and log files can be equal to the space that is required for the database.

If there's insufficient disk space available, a message appears indicating that an error occurred during the execution of a custom action: `_CreateDatabase`. The installation stops before permanent changes are made. If you examine the Service Manager setup log, you find the following string:

```
Additional Error Description : MODIFY FILE encountered operating system error 112(There is not enough space on the disk.) while attempting to expand the physical file
```

You've to either increase the amount of free disk space that is available or reduce the amount of space that Service Manager allocates for the database, and then attempt the installation again. If you're installing Service Manager in a nonproduction environment, you can specify as little as 500 MB for the database.

## Next steps

To deploy Service Manager using command-line parameters, review [Deploy Service Manager from a command line](deploy-cmd-line.md).
