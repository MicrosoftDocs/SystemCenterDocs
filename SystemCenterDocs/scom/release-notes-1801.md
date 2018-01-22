---
title: System Center Operations Manager 1801 Release Notes
description: This article describes issues and workarounds for System Center 1801 - Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/16/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.assetid: 
ms.technology: operations-manager
ms.topic: article
---

# System Center Operations Manager 1801 Release Notes

The following release notes apply to System Center Operations Manager 1801.

## Telemetry for HTML5 dashboards
**Description:** Usage telemetry for HTML5 dashboards are collected through Application Insights. For more information on what user telemetry is collected by Application Insights, see [Usage analysis with Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-usage-overview).

**Workaround:** Disable monitoring of the Web console using the Operations Manager Web Application Transaction Monitoring template.   

## Edit Company Knowledge
**Description:** If the company knowledge of an alert/monitor/rule is already saved while editing in the Operations console and then the company knowledge of the same alert/monitor/rule is edited and saved using the new HTLM5 dashboards in the Web console, the content that was saved originally using the Operations console is overridden with the content saved through the Web console.

**Workaround:** None

## Access Silverlight dashboards in Web Console using a different URL
**Description:** With HTML5 dashboards in Operations Manager 1801, the entire Web console is HTML based. Silverlight dashboards cannot be displayed in the Web console. To access  existing Silverlight dashboards, you have to access using the following URL using Internet Explorer with Silverlight enabled - `http(s)://<Servername>/dashboard` and this will display all Silverlight dashboards. 
