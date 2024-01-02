---
title: How to Configure Grooming Settings for the Operations Manager Database
description: This article reviews the default grooming settings for the operational database and how to modify those settings.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 09/26/2023
ms.custom: UpdateFrequency3, engagement-fy24
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
ms.assetid: ccbc61b1-4919-4514-ac2e-ea68384e3be8
---

# How to configure grooming settings for the Operations Manager database

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

The grooming process removes unnecessary data from the Operations Manager database in order to maintain performance by managing its size. You can configure the grooming setting for the following data types:  

-   Resolved alerts  

    > [!NOTE]  
    > Active alerts are never groomed. You must close an alert before it'll be groomed.  

-   Event data  

-   Performance data  

-   Task history  

-   Monitoring job data  

-   State change events data  

-   Performance signature  

-   Maintenance mode history  

-   Availability history  

Any updates to the grooming settings are applied immediately.  

Use the following procedure to specify when specific data types are deleted or groomed from the Operations Manager database in a management group. The default grooming setting for all data types is data older than seven days.  

## To configure database grooming settings for a management group  

1.  In the Operations console, select **Administration**.  

2.  In the navigation pane, expand **Administration**, and select **Settings**.  

3.  In the **Settings** pane, right-click **Database Grooming**, and select **Properties**.  

4.  In the **Global Management Group Settings - Database Grooming** dialog, select a data type, and select **Edit**.  

5.  In the dialog for the record type, specify **Older than** days, and select **OK**.  

6.  In the **Global Management Group Settings - Database Grooming** dialog, select another data type to **Edit** or select **OK**.  

## Next steps

- To learn more about the default retention period for the different data types stored in the Operations Manager Reporting data warehouse database and how to modify those settings, see [How to configure grooming settings for the Operations Manager Reporting data warehouse database](manage-omdwdb-grooming-settings.md).
