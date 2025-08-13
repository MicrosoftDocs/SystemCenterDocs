---
title: Personalize a View in Operations Manager
description: This article describes how to customize views in the Operations Manager Operations console.
ms.date: 04/23/2025
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: aa50d20a-5f38-476f-b79c-8f2f99e4ff1f
---

# Personalize a view in Operations Manager


This article describes how to customize views in the Operations Manager Operations console.

In System Center Operations Manager, views are contained in management packs. If a view is contained in a sealed management pack, you can open the properties of the view, but you can't save any changes to it. However, you can change the display options of the view and then save it as a personalized view.  

> [!NOTE]  
> Personalized views are only visible to the user who personalized the view.  

## Personalize a view

To personalize a view, follow these steps:

1. In the Operations console, select **Monitoring**.  

2. In the **Monitoring** workspace, right-click the view that you want to personalize and then select **Personalize view**. The **Personalize view** dialog displays with the default settings of the view.  

3. In **Columns to display**, click to place a check next to the property that you want to display in your view. You can also click to remove any checkmarks set by the original view. In the **Sort columns by** box, select the dropdown arrow to choose a property by which you want to sort the monitored objects in your view, and select **OK**.  

    > [!NOTE]  
    > In a state view, the option to sort by groups isn't available. This option is available in other view types, such as the alert view and event view.  

## Restore view defaults 

To restore view defaults, follow these steps:

1. In the Operations console, select **Monitoring**.  

2. In the **Monitoring** workspace, right-click the personalized view.  

3. Select **Reset to Default**, and select **OK**.  

## Next steps

- You can use views and dashboards to visualize operational data from different perspectives to make meaningful decisions. To understand how to do this, see [Use views and dashboards in Operations Manager](manage-console-using-views-dashboards.md).  

- Operations Manager includes many views that are created during installation. To understand what these views provide, see [Standard views in Operations Manager](manage-console-standard-views.md).  

- To understand how to create your own custom views and dashboards in Operations Manager, as well as how to scope them, see [Create and scope views in Operations Manager](manage-console-scope-views.md).  
