---
ms.assetid: 
title: Integrate Azure Monitor SCOM Managed Instance (preview) with Log Analytics
description: This article details about the Integration of Azure Monitor SCOM Managed Instance (preview) with Log Analytics  
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: mkluck
ms.date: 10/04/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Integrate Azure Monitor SCOM Managed Instance (preview) with Log Analytics

The integration of Azure Monitor SCOM Managed Instance with Log Analytics (LA) is a mechanism to synchronize the monitoring data from individual SCOM Managed Instances to the respective LA workspace with a defined frequency, enabling retention and advanced user actions such as visualization and reporting.

Synchronization of SCOM Managed Instance monitoring data to a common data source (LA) helps to centralize all monitoring logs and prevents data fragmentation. With LA retention policies, longer-term trend analysis is possible in LA.

## General guidelines

Following are the general guidelines for the location and existence of LA workspaces and SCOM Managed Instance:

- To reduce latency in data synchronization, we recommend that you keep the SCOM Managed Instance and LA workspace in the same region.

- To reduce management (RBAC, policies, NSG) activities, we recommend that you keep SCOM Managed Instance and LA workspace in the same subscription and resource group.

- To reduce onboarding failures on LA integration, the SCOM Managed Instance creation prerequisite script checks if you have the permission to create LA workspace on Azure (Microsoft.Resources/deployments/*, Microsoft.OperationalInsights/workspaces/*). For more information, see [Manage access to Log Analytics workspace](/azure/azure-monitor/logs/manage-access?tabs=portal).

## Permissions required

To set up LA integration, the minimum privilege required is **Log Analytics Contributor** or **Monitoring Contributor at Resource Group scope**.

**Data synchronized to Log Analytics workspace**

The prioritized list of SCOM Managed Instance monitored data that synchronizes to LA workspace are  

- **EVENT**: Table consists of Event log data collected by management pack rules and monitors.
- **STATE**: Table consists of current and past health states of monitored resources.
- **PERFORMANCE**: Table consists of Performance metric data collected by management pack rules and monitors.
- **AUDIT**: Table consists of management pack related audit (change tracking) data.

## Data Retention in Log Analytics

The retention policy application on Log Analytic workspace is default value, which is 30 days. Azure Monitor SCOM managed instance doesn't change this value. For more information on Data retention, see [Data retention and archive in Azure Monitor Logs](/azure/azure-monitor/logs/data-retention-archive?tabs=portal-1%2Cportal-2)

:::image type="Data retention" source="media/integrate-scom-managed-instance-with-log-analytics/data-retention.png" alt-text="Screenshot that shows about Data retention.":::