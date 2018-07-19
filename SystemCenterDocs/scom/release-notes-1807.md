---
title: System Center Operations Manager 1807 Release Notes
description: This article describes issues and workarounds for System Center Operations Manager 1807.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 07/11/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1807'
ms.assetid: 
ms.technology: operations-manager
ms.topic: conceptual
---

# System Center Operations Manager 1807 Release Notes

The following release notes apply to System Center Operations Manager 1807.

## Log rotation for Linux agent
**Description:** SCX logs fill up frequently, which eventually consumes all available free space on the system disk.  As a result, the system becomes unresponsive unless the logs are cleaned up manually.  To address this issue, we have introduced a logrotate feature for SCX agent. This will help you rotate old logs and save disk space.

**Prerequisite:** Logrotate is located in /usr/sbin/logrotate by default on Linux platforms.

**Workaround:** During scxagent installation we push the following logrotate conf file to `/etc/logroate.d` location. To modify, you should make changes to the `/etc/logrotate.d/scxagent` config file. The current configured values will archive the five most recent log files and delete the old logs. A logfile which has reached 50 MB in size is also deleted. We have included one cron config file at `/etc/cron.d` location. With this configuration, the logrotate process executes every four hours. To customize the configuration, you need to modify these two files. Please look at man page for [cron](https://linux.die.net/man/5/crontab) and [logrotate](https://linux.die.net/man/8/logrotate) for further details.

The following is the default configuration for the SCX agent.

```
/var/opt/microsoft/scx/log/*/scx.log
{	 
rotate 5
missingok
notifempty
nodatext
compress
size 50M
copytruncate
postrotate
/usr/sbin/scxadmin -log-rotate
all
}	
```

>[!NOTE]
>If SELinux is already installed, SCX installer pushes a SELinux module that will enable logrotate. For scenarios where SElinux is enabled after agent installation, you have to import SELinux module for logrotate to work.

## Support for SQL Server 2017

**Description**: With version 1807, SQL Server 2017 is supported only if it is upgraded from SQL Server 2016.  A fresh installation of SQL Server 2017 with version 1807 is not supported.  If you already have version 1801 deployed with SQL Server 2016, you need to apply Operations Manager version 1807 before performing an upgrade to SQL Server 2017.  

**Workaround**: Before upgrading to SQL Server 2017, review the following article about the upgrade process - [Upgrade Operations Manager 1807 databases to SQL Server 2017](upgrade-sqlserver-2017-opsmgr-1807.md). 

## Supportability with Internet Explorer Compatibility View

**Description**: The HTML5 Web console does not support Internet Explorer Compatibility View.  

**Workaround**: None

## Support for Operations Manager and Service Manager console coexistence

**Description**:  With System Center version 1801, installing the Service Manager console on a Operations Manager management server wasn't supported.  This would cause the SDK service to prematurely stop.  

**Workaround**:  To co-locate the Operations Manager and Service Manager console on the same computer, they must be running version 1807.  

