---
title: How to Personalize a View in Operations Manager
description: This article describes how to customize views in the Operations Manager Operations console.  
author: mgoedtel
ms.author: magoedte
ms.manager: carmonm
ms.date: 11/28/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: aa50d20a-5f38-476f-b79c-8f2f99e4ff1f
---

# How to personalize a view in Operations Manager

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, views are contained in management packs. If a view is contained in a sealed management pack, you can open the properties of the view but you cannot save any changes to it. However, you can change the display options of the view and then save it as a personalized view.  
  
> [!NOTE]  
> Personalized views are only visible to the user who personalized the view.  
  
## To personalize a view  
  
1.  In the Operations console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, right-click the view that you want to personalize and then click **Personalize view**. The **Personalize view** dialog box displays with the default settings of the view.  
  
3.  In **Columns to display**, click to place a check next to the property that you want to display in your view. You can also click to remove any checkmarks set by the original view. In the **Sort columns by** box, click the drop-down arrow to choose a property by which you want to sort the monitored objects in your view, and then click **OK**.  
  
    > [!NOTE]  
    > In a state view, the option to sort by groups is not available. This option is available in other view types, such as the alert view and event view.  
  
## To restore view defaults  
  
1.  In the Operations console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, right-click the personalized view  
  
3.  Click **Reset to Default**, and then click **OK**.  
  
## Next steps

- You can use views and dashboards to visualize operational data from different perspectives to make meaningful decisions.  To understand how to do this, see [Using Views and Dashboards in Operations Manager](manage-console-using-views-dashboards.md).  

- Operations Manager includes a number of views that are created during installation.  To understand what these views provide, see [Standard Views in Operations Manager](manage-console-standard-views.md).  

- To understand how to create your own custom views and dashboards in Operations Manager,  as well as how to scope them, see [Creating and Scoping Views in Operations Manager](manage-console-scope-views.md).  
