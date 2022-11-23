---
ms.assetid: 
title: How to create reports on Power BI
description: This article describes how to create reports on Power BI for Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/23/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# How to create reports on Power BI?

This article describes how to create reports on Power BI for Azure Monitor SCOM Managed Instance (preview).

## Prerequisites

- Azure Active Directory based authentication: 

    - Create an Azure Active Directory group for the people whom you want to provide permissions to read the SQL managed instance through this Power BI report. 

    - Create login for the above created Azure Active Directory group in the SQL managed instance, which adds the user principal of the group in SQL managed instance. For more information, see [Create Login (Transact-SQL)](/sql/t-sql/statements/create-login-transact-sql?view=azuresqldb-mi-current&preserve-view=true).

- SQL based authentication: 

    - For SQL based authentication, you need the username and password of the SQL managed instance.

## Create reports through public endpoint of SQL MI

1. Sign into the Azure portal and search for SCOM Managed Instance (preview). SCOM Managed Instance (preview) overview page opens.
1. On the Overview page, under Reports, select **Power BI**. You have three options on the Power BI page.
    1. **Prerequisite**: Allows you to Manage endpoints.
    1. **Configure and install Power BI**: Allows you to install and configure the SCOM Managed Instance (preview) dashboard in Power BI.
    1. **View Power BI dashboard**: Allows you to visualize the SCOM Managed Instance (preview) dashboard in Power BI after the configuration.
         :::image type="SCOM MI Power BI page" source="media/operations-manager-managed-instance-create-reports-on-power-bi/scom-mi-power-bi.png" alt-text="Screenshot of SCOM MI Power BI page.":::
        1. The app prepopulates the data. You can add parameter values such as **Data-Warehouse DB host URL** which is the public endpoint and **Data-Warehouse Name** which is the database name. 
            >[!Note]
            >If you want to update these parameters, go to **Settings** of the dataset, and edit the parameters. 
        1. After you enter the parameters, select any one of the following authentication methods:
            - SQL username and password-based method
            - Azure Active Directory based method 
            The dataset will get refreshed and reports will be refreshed from the dataset. 

## Next steps

> [!div class="nextstepaction"]
> [Operations Manager managed instance (preview) overview](operations-manager-managed-instance-overview.md)

