---
title: How to Personalize a View in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa50d20a-5f38-476f-b79c-8f2f99e4ff1f
---
# How to Personalize a View in Operations Manager
In [!INCLUDE[om12long](../Token/om12long_md.md)], views are contained in management packs. If a view is contained in a sealed management pack, you can open the properties of the view but you cannot save any changes to it. However, you can change the display options of the view and then save it as a personalized view.

> [!NOTE]
> Personalized views are only visible to the user who personalized the view.

### To personalize a view

1.  In the Operations console, click **Monitoring**.

2.  In the **Monitoring** workspace, right\-click the view that you want to personalize and then click **Personalize view**. The **Personalize view** dialog box displays with the default settings of the view.

3.  In **Columns to display**, click to place a check next to the property that you want to display in your view. You can also click to remove any checkmarks set by the original view. In the **Sort columns by** box, click the drop\-down arrow to choose a property by which you want to sort the monitored objects in your view, and then click **OK**.

    > [!NOTE]
    > In a state view, the option to sort by groups is not available. This option is available in other view types, such as the alert view and event view.

### To restore view defaults

1.  In the Operations console, click **Monitoring**.

2.  In the **Monitoring** workspace, right\-click the personalized view

3.  Click **Reset to Default**, and then click **OK**.

## See Also
[Using Views in Operations Manager](../Topic/Using-Views-in-Operations-Manager.md)
[Standard Views in Operations Manager](../Topic/Standard-Views-in-Operations-Manager.md)
[Creating Views in Operations Manager](../Topic/Creating-Views-in-Operations-Manager.md)
[Guidance for Scoping and Targeting Views](../Topic/Guidance-for-Scoping-and-Targeting-Views.md)

