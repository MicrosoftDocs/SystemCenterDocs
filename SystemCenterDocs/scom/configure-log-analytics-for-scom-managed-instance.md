---
ms.assetid: 
title: Configure Log Analytics for Azure Monitor SCOM Managed Instance
description: This article describes how to configure Azure Monitor SCOM Managed Instance with Azure Log Analytics.
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

# Configure Log Analytics for Azure Monitor SCOM Managed Instance

This article describes how to configure Azure Monitor SCOM Managed Instance with Azure Log Analytics.

Before you configure Log Analytics workspace for SCOM managed instance, create a Log Analytics workspace. For more information on how to create Log Analytics workspace, see [Create a Log Analytics workspace](/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-portal).

## Prerequisites

Ensure to provide Log Analytics Contributor permissions on the Log Analytics workspace's resource group for Microsoft.SCOM Resource Provider (RP).

To provide the permissions, follow these steps:

1. Navigate to the resource group of respective Log analytics workspace > **Access Control** > **Add Role Assignment** > **Choose Log Analytics Contributor** and select **Next**.

2. Search for **Microsoft.SCOM Resource provider** and select **Assign**.

## Configure Log Analytics Workspace for SCOM Managed Instance

To integrate SCOM Managed Instance with Log Analytics, follow these steps: 

1. Sign in to the [Azure portal](https://ms.portal.azure.com/#home). Search for and select **SCOM Managed Instance**.

2. On the **Overview** page, select **View Instances**.

3. On the **SCOM managed instances** page, select the desired SCOM managed instance.  

4. On the left pane, select **Log Analytics workspace**.

5. On the **Log Analytics workspace** page, select **Link Log Analytics workspace**.

6. On the **Configure Log Analytics Workspace for SCOM managed instance** page, do the following:

     1. **Destination details**:
         - **Subscription**: Select the desired subscription.
         - **Log Analytics workspace**: Select the desired Log Analytics workspace.

             >[!NOTE]
             >Ensure to provide Log Analytics Contributor permissions on the resource group.  

     2. **Log data types**:
         - **Data types**: Select the desired date type.  

     3. **Historic data**:
         - **Enable historic data for last 7 days**: Select this checkbox if you wish to enable the last seven days of historic data.

7. Select **Save**.

It takes 2-3 minutes for the integration of SCOM managed instance with Log Analytics. 

## View Logs

To view the integrated logs, follow these steps:

1. Post successful configuration, wait for a few minutes, and sign in to the [Azure portal](https://ms.portal.azure.com/#home). Search for and select **Log Analytic workspace**.

2. On the **Overview** page, select **Logs**.
   On the Query page, under **Custom Logs**, SCOM Managed Instance related data tables such as State, Performance, Event, and Management pack (ending with CL) are created.

3. Select the desired custom table (State, Performance, Event and Management pack) and select Run to view the results.

Optionally, you can create a new workbook, query the data from this LA workspace, and visualize the monitored data.

For more information on Log Analytics workspaces, see the following articles:

- [Log Analytics workspace overview](/azure/azure-monitor/logs/log-analytics-workspace-overview).
- [Monitor Log Analytics workspace health](/azure/azure-monitor/logs/log-analytics-workspace-health).