---
ms.assetid: d15240cb-f087-4641-a65d-b0b48469f208
title: include file
description: include file to describe the new features in Operations Manager 1801
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 12/21/2018
ms.service: system-center
monikerRange: 'sc-om-1801'
ms.subservice: operations-manager
ms.topic: include
ms.update-cycle: 1095-days
---

## New features in Operations Manager 1801

The contents in the following sections describe new features in System Center 1801 - Operations Manager.

## Enter product key from the Operations console

In the previous versions of Operations Manager, you had to upgrade from the evaluation version to a licensed version using the PowerShell cmdlet **Set-SCOMLicense** after the initial deployment of a new management group.  Registering the product key can now be performed during or after setup in the Operations console. The PowerShell cmdlet **Set-SCOMLicense** has been updated to support registering the license key remotely from a management server.

## Linux monitoring

You can now use a Linux agent with FluentD support for log file monitoring at par with Windows Server. This update provides the following improvements over previous log file monitoring:

- Wildcard characters in log file name and path.
- New match patterns for customizable log search like simple match, exclusive match, correlated match, repeated correlation, and exclusive correlation.
- Support for generic Fluentd plugins published by the fluentd community.

## Improved HTML5 dashboarding experience
The Web console has been redesigned and is now a fully HTML-based console and no longer has a dependency on Silverlight.  The new dashboards have been redesigned with:  

* Modern user interface
* Simplified widget and dashboard authoring
* Accessible from multiple browsers
* Enhanced troubleshooting experience with drill-down pages
* Extensibility with a custom widget using a new [REST API](/rest/operationsmanager)
* Export and share dashboards

Network authentication is enabled with the new web console.  

## System Center Visual Studio Authoring Extension (VSAE) support for Visual Studio 2017
Visual Studio Authoring Extension (VSAE) is now updated to be compatible with Visual Studio(VS) 2017. Management Pack (MP) developers can continue using it with the latest version of Visual Studio to create custom management packs and use one of the MP templates provided, or edit an existing MP.

## Enhanced SDK Client performance
We've introduced performance improvements in the Operations console that typically prevent the console from responding while a new management pack is being imported or deleted, or a configuration change to an MP is saved.  

## Updates and recommendations for third-party Management Packs

In System Center 2016, we released the MP Updates and Recommendations feature, which has been extended to include discovery and downloads of third-party management pack updates based on feedback from customers.

## Linux Kerberos support
Operations Manager can now support Kerberos authentication wherever the WS-Management protocol is used by the management server to communicate with UNIX and Linux computers, providing greater security by no longer needing to enable basic authentication for Windows Remote Management (WinRM).

## Service Map integration
Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services. It automatically builds a common reference map of dependencies across your servers, processes, and third-party services. Integration between Service Map and System Center Operations Manager allows you to automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map. For more information on planning and configuring  integration, see [Service Map integration with System Center Operations Manager](/azure/operations-management-suite/operations-management-suite-service-map-scom).