---
title: include file
description: include file to summarize the release notes for OM 1807.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 07/25/2018
ms.service: system-center
ms.assetid: 4f84c864-ef52-4e81-a186-a03bf15b266e
ms.subservice: operations-manager
ms.topic: include
---

## Operations Manager 1807 release notes

The following sections summarize the release notes for Operations Manager 1807 and include the known issues and workarounds. For more information about version 1807 and what issues are addressed, see [KB4133779](https://support.microsoft.com/help/4133779).

## Log rotation for Linux agent
**Description**: Under certain scenarios, the SCX logs fill up frequently, which eventually consumes all the available free space on the system disk. As a result, the system becomes unresponsive unless the logs are cleaned up manually. To address this issue, we've introduced a logrotate feature for SCX agent. This will help you rotate old logs and save disk space.

**Prerequisite**: Logrotate is located in `/usr/sbin/logrotate` by default on Linux platforms.

**Workaround**: During scxagent installation, we push the following logrotate conf file to `/etc/logroate.d` location.

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

You can change the default values to support your requirements. The default configured values will rotate the scx.log file if scx.log file size reaches 50 MB. We've included one cron config file at `/etc/cron.d` location.  With this configuration, the logrotate process executes every four hours. To customize the configuration, you need to modify these two files. Review the man page for [cron](https://linux.die.net/man/5/crontab) and [logrotate](https://linux.die.net/man/8/logrotate) for further details.

>[!NOTE]
>If SELinux is already installed, SCX installer pushes a SELinux module that will enable logrotate. For scenarios where SElinux is enabled after agent installation, you've to import SELinux module for logrotate to work.

## Support for SQL Server 2017

**Description**: With version 1807, SQL Server 2017 is supported only if it's upgraded from SQL Server 2016. A fresh installation of SQL Server 2017 with version 1807 isn't supported.  If you already have version 1801 deployed with SQL Server 2016, you need to apply Operations Manager version 1807 before performing an upgrade to SQL Server 2017.  

**Workaround**: Before upgrading to SQL Server 2017, review the following article about the upgrade process - [Upgrade Operations Manager 1807 databases to SQL Server 2017](../scom/upgrade-sqlserver-2017-opsmgr.md).

>[!NOTE]
>
>From SQL Server Reporting Services (SSRS) 2017 version 14.0.600.1274 and later, the default security settings don't allow resource extension uploads. This leads to **ResourceFileFormatNotAllowedException** exceptions in Operations Manager during the deployment of reporting components.
>
>To fix this, open SQL Management Studio, connect to your Reporting Services instance, open **Properties**>**Advanced**, and add \*.\* to the list for *AllowedResourceExtensionsForUpload*. Alternatively, you can add the full list of Operations Manager's reporting extensions to the *allow list* in SSRS.

## Supportability with Internet Explorer Compatibility View

**Description**: The HTML5 Web console doesn't support Internet Explorer Compatibility View.  

**Workaround**: None

## Support for Operations Manager and Service Manager console coexistence

**Description**: With System Center version 1801, installing the Service Manager console on an Operations Manager management server wasn't supported. This would cause the SDK service to prematurely stop.  

**Workaround**: To co-locate the Operations Manager and Service Manager console on the same computer, they must be running version 1807.  

## Upgrade to Operations Manager version 1807
To understand the requirements and steps to successfully upgrade your Operations Manager version 1801 management group to version 1807, review [How to upgrade to Operations Manager version 1807](../scom/upgrade-1801-to-1807.md).

## OpenSSL 1.1.0 version support

**Description**: On Linux platforms, OpenSSL 0.9.8 support is dropped.

**Workaround**: We've added support for OpenSSL 1.1.0.
