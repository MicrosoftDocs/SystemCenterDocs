---
ms.assetid: 
title: Create reports on Power BI
description: This article describes how to create reports on Power BI for Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/25/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create reports on Power BI

This article describes how to create reports on Power BI for Azure Monitor SCOM Managed Instance (preview).

## Prerequisites

- Azure Active Directory based authentication: 

    - Create an Azure Active Directory group for the users to whom you want to provide permissions to read the SQL managed instance through this Power BI report. 

    - Create sign in credentials for the Azure Active Directory group in the SQL managed instance created above, which adds the user principal of the group in the SQL managed instance. For more information, see [Create Login (Transact-SQL)](/sql/t-sql/statements/create-login-transact-sql?view=azuresqldb-mi-current&preserve-view=true).

- SQL based authentication: 

    - For SQL based authentication, you need the username and password of the SQL managed instance.

## Create reports through public endpoint of SQL MI

1. Sign into the Azure portal and search for SCOM Managed Instances (preview). The SCOM Managed Instance (preview) Overview page opens.
1. On the **Overview** page, under **Reports**, select **Power BI**. You have three options on the Power BI page.
    1. **Prerequisite**: Allows you to manage endpoints.
    1. **Configure and install Power BI**: Allows you to install and configure the SCOM Managed Instance (preview) dashboard in Power BI.
    1. **View Power BI dashboard**: Allows you to visualize the SCOM Managed Instance (preview) dashboard in Power BI after the configuration.
1. Review the **Prerequisites** to ensure Public endpoint of SQL MI is enabled. You will notice the Database Host URL and Database name are displayed.
     :::image type="Public endpoints" source="media/operations-manager-managed-instance-create-reports-on-power-bi/public-endpoins.png" alt-text="Screenshot showing public endpoints.":::
1. Select **Configure Dashboard**, **Powerbi.com** opens in a new browser. Select **Get it now** to install **Microsoft SCOM managed instance reports** Power BI app in your workspace. 
     :::image type="Power BI app" source="media/operations-manager-managed-instance-create-reports-on-power-bi/power-bi-app.png" alt-text="Screenshot showing Power BI app.":::
1. The app displays sample data. You can edit the parameter values **Data-Warehouse DB host URL** and **Data-Warehouse Name**.
     >[!Note]
     >To update the parameters, go to **Settings** of the dataset, and edit the parameters or select **Connect your data** in the banner.
     :::image type="Connect your data" source="media/operations-manager-managed-instance-create-reports-on-power-bi/connect-your-data.png" alt-text="Screenshot showing Connect your data option.":::
1. After you enter the parameters, select any one of the following authentication methods: 
    - SQL username and password-based method 
    - Azure Active Directory based method 
    The dataset and reports will be refreshed. 

     >[!Note]
     >To view Power BI reports of multiple SCOM Managed Instances (preview), **Microsoft SCOM managed instance reports** app must be installed individually in different Power BI workspace.

## Next steps

> [!div class="nextstepaction"]
> [Operations Manager managed instance (preview) overview](operations-manager-managed-instance-overview.md)

