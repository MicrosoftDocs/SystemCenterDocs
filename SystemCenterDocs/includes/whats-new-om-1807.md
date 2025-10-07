---
ms.assetid: 70fad9da-0c8b-4b0a-abbd-a1246b57da5b
title: include file
description: include file to describe the new features in Operations Manager 1807.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 12/21/2018
ms.custom: na
ms.service: system-center
monikerRange: 'sc-om-1807'
ms.subservice: operations-manager
ms.topic: include
---

## New features in Operations Manager 1807

The content in the following sections describes new features in System Center 1807 - Operations Manager.

>[!NOTE]
> To view the bugs fixed and the installation instructions for Operations Manager 1807, see [KB article 4133779](https://support.microsoft.com/help/4133779).

## Configure APM component during agent install or repair
In System Center Operations Manager version 1801 agent, the Application Performance Monitoring (APM) feature could cause a crash with IIS Application pools and could crash the SharePoint Central Administration v4 application pool running .NET Framework 2.0, preventing it from starting. You can now disable the APM component when you deploy the Operations Manager agent from Discovery Wizard in the console, when performing a repair of the agent from the Operations console and similarly controlling behavior when using the PowerShell cmdlets **Install-SCOMAgent** and **Repair-SCOMAgent**.  


## Linux log rotation

To prevent the SCX logs from growing and consuming all the available free space on the system disk, a log rotation feature is now available for the SCX agent.  

## HTML5 Web console enhancements
The following improvements are provided in the Web console for version 1807:

* Added the PowerShell widget.
* Includes an effective configuration widget in the Monitoring objects detail page showing the running rules and monitors and override settings applied.
* Network node/network interface drill-down is now available as a tab when you select a network device and drill down to the Monitoring objects detailed page. It delivers the same experience as what is available in the Operations console.
* Alert widget enhancement includes an improved layout and presentation of alert details. You can modify the resolution state and drill down to the Monitoring object details page for the alert source.
* The monitoring tree can be hidden when a dashboard is integrated with SharePoint.
* The size of the health icon can be changed in the Topology widget.
* Managing maintenance schedules can be accomplished in the Web console matching the experience in the Operations console.
* User and operators can create dashboards in My Workspace.

## Support for SQL Server 2017
With version 1807, upgrading from SQL Server 2016 to SQL Server 2017 is supported. To understand the requirements and steps to successfully upgrade your Operations Manager version 1801 management group to version 1807, review [How to upgrade to Operations Manager version 1807](../scom/upgrade-1801-to-1807.md).

## Operations Manager and Service Manager console coexistence
The Operations and Service Manager version 1807 consoles and PowerShell modules can be installed on the same system.  

## OpenSSL 1.1.0 version support
On Linux platforms, OpenSSL 0.9.8 support is dropped and we've added support for OpenSSL 1.1.0.

## Ubuntu 18 and Debian 9 support
These Linux platforms are added to our support matrix for monitoring UNIX and Linux computers.

## Auto detection of Pseudo FS and drop Enumeration.
The UNIX and Linux agent has been enhanced to detect pseudo file system dynamically and ignore enumeration.  
