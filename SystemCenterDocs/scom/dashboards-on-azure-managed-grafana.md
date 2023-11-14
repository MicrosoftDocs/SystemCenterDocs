---
ms.assetid: 
title: Dashboards on Azure Managed Grafana
description: This article describes how to create a SCOM Managed Instance dashboard on Azure Managed Grafana.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/14/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Dashboards on Azure Managed Grafana

Azure Managed Grafana (AMG) is a data visualization platform, built on top of the Grafana software by Grafana Labs. Grafana helps you bring together metrics, logs, and traces into a single user interface.

Azure Managed Grafana is optimized for the Azure environment and works seamlessly, providing the following integration features:

- Built-in support for [Azure Monitor](https://learn.microsoft.com/azure/azure-monitor/) and [Azure Data Explorer](https://learn.microsoft.com/azure/data-explorer/).
- User authentication and access control using Microsoft Entra identities.
- Direct import of existing charts from the Azure portal.

This article describes how to create a SCOM Managed Instance dashboard on Azure Managed Grafana.

## Steps to create a SCOM Managed Instance dashboard on Azure Managed Grafana

To create a SCOM Managed Instance dashboard on Azure Managed Grafana, follow these steps:

### Get started with Azure Managed Grafana

1. Get started by using an Azure Managed Grafana (AMG) with a version 10 on the Azure portal. To create an AMG instance, follow [these steps](https://learn.microsoft.com/azure/managed-grafana/quickstart-managed-grafana-portal). Optionally, you can reuse an existing AMG instance.
2. Enable System assigned managed identity on the AMG instance.

     :::image type="Permissions" source="media/dashboards-on-azure-managed-grafana/grafana-permissions.png" alt-text="Screenshot of grafana permissions.":::

### Assign Permissions

1. On the AMG instance, provide **Grafana Editors** permissions to the users who need access to create dashboards.
2. Grant permissions to the managed identity of the Grafana instance on the SQL managed instance database.
3. [Download and run the PowerShell script](https://go.microsoft.com/fwlink/?linkid=2252607) to create SQL user for Azure Managed Grafana identity.
4. Note the SQL managed instance public endpoints and the Database name.

### Configure Data source on AMG

1. Browse to the AMG portal by selecting the AMG instance endpoint.
2. Navigate to **Connections** > **Data sources** and add a data source of type **Microsoft SQL Server**.
3. On the **Settings** page, enter the Database endpoint URL in the **Host** field.
4. Enter the Database name (noted above) in **Database** field.
5. Use Azure Managed Identity as the authentication method.

### Import SCOM Managed Instance dashboards in AMG instance

1. Navigate to AMG instance endpoint > **Dashboards** > **New** > **Import** > **Import via grafana.com** > **Enter 19919** and select **Import**.
2. Browse to the imported dashboards.
3. Choose the above created Data source and the respective database in the dashboard settings.