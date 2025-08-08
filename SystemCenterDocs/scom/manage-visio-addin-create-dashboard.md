---
title: Build a simple Monitoring Dashboard using the Visio Web Part
description: This article provides a walk-through on how to create a basic monitoring dashboard in SharePoint linking to your Visio drawing.
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.date: 08/07/2025
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: 21d8f3a5-2ac8-4776-b063-f6895a21cd5a

---

# Build a simple monitoring dashboard using the Visio Web Part



SharePoint Enterprise edition includes a Web part for Visio Services called the Visio Web Access Web Part. You can add this Web part to any SharePoint Web part page to build a dashboard that uses published Visio diagrams to provide visualizations.  

## Build a monitoring dashboard for your Visio diagram 

To build a monitoring dashboard for your Visio diagram, follow these steps:

1. In Internet Explorer, navigate to your SharePoint site.  

2. Navigate to the Shared Documents document library.  

3. Select **Site Actions** (above the ribbon), and select **More Options**.  

4. Select the Web Part page and select **Create**.  

5. Enter a name for the new page.  

6. Under **Layout**, select **Header, Right Column, Body** from the list of available layout templates.  

7. Select **Create** to create the new Web page.  

8. Select the Body zone. You should see a new **Insert** tab on the ribbon.  

9. On the **Insert** tab, select **Web Part**.  

10. In the **Categories** list, select **Business Data**, and then, in the **Web Parts** list, select **Visio Web Access**.  

11. Select **Add**.  

    The Visio Web Access Web Part is added to the Body zone of the Web part page.  

12. Edit the properties of the Visio Web Access Web Part. In the **Web Part** toolbar, select **Edit Web Part**.  

13. Set the **Web Drawing URL** property. Select Browse and navigate to the document library where you published a Visio diagram. Select the published diagram and select **OK**.  

14. Set the **Automatic Refresh** property to 1 minute (the minimum value supported). This enables the dashboard to automatically refresh the diagram with new data from the management server every 1 minute.  

15. Clear the **Show Open in Visio** option in the Toolbar and User Interface section.  

16. Select **OK** to apply the changes.  

    You should now see the rendered Visio diagram in the browser.  

17. Select **Stop Editing** to exit edit mode.  

Your Web part should now display with the published diagram in the Visio Web Access Web part. Notice that the **Open in Visio** button (normally available by default) is no longer available in the Web part toolbar.  

## Next steps

Learn how to [publish Visio diagrams] that you’ve connected to Operations Manager data to a SharePoint document library(manage-visio-addin-publish-sharepoint.md).
