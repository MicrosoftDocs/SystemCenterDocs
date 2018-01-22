---
ms.assetid: 
title: What's New in Operations Manager - 1801
description: This article describes what's new in System Center 1801 - Operations Manager compared to previous versions. 
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/16/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.technology: operations-manager
ms.topic: article
---

# What's New in System Center 1801 - Operations Manager

The content in this section describes what's new and changed in System Center 1801 - Operations Manager.

## Enter product key from the Operations console

In previous versions of Operations Manager you had to upgrade from the evaluation version to a licensed version using the PowerShell cmdlet **Set-SCOMLicense** after initial deployment of a new management group.  Registering the product key can now be performed during or after setup in the Operations console. The PowerShell cmdlet **Set-SCOMLicense** has been updated to support registering the license key remotely from a management server.


 or after evaluation version has expired.  

## Linux monitoring 

You can now use a Linux agent with FluentD support for log file monitoring at par with Windows Server.  This update provides the following improvements over previous log file monitoring:

- Wild card characters in log file name and path.
- New match patterns for customizable log search like simple match, exclusive match, correlated match, repeated correlation, and exclusive correlation.
- Support for generic Fluentd plugins published by the fluentd community.

## Improved HTML console experience

The Web console has been redesigned and is now a fully HTML-based console and no longer has a dependency on Silverlight.  The monitoring tree and dashboards support the HTLM5 markup language.  

## Enhanced SDK Client performance 
We have introduced performance improvements in the Operations console that typically prevent the console from responding while a new management pack is being imported or deleted, or a configuration change to an MP is saved.  

## Updates and recommendations for third-party Management Packs

In System Center 2016 we released the MP Updates and Recommendations feature, which has been extended to include discovery and downloads of third-party management pack updates, based on feedback from customers. 

## Linux Kerberos support 
Operations Manager can now support Kerberos authentication wherever the WS-Management protocol is used by the management server to communicate with UNIX and Linux computers, providing greater security by no longer needing to enable basic authentication for Windows Remote Management (WinRM). 


## Service Map integration
Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services. It automatically builds a common reference map of dependencies across your servers, processes, and third-party services. Integration between Service Map and System Center Operations Manager allows you to automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.  For further information on planning and configuring  integration, see [Service Map integration with System Center Operations Manager](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-service-map-scom).  
