---
title: Build a simple monitoring dashboard using the Visio Web Part
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21d8f3a5-2ac8-4776-b063-f6895a21cd5a
---
# Build a simple monitoring dashboard using the Visio Web Part
SharePoint 2010 Enterprise edition includes a Web part for Visio Services called the Visio Web Access Web Part. You can add this Web part to any SharePoint Web part page to build a dashboard that uses published Visio diagrams to provide visualizations.

### To build a monitoring dashboard for your Visio diagram

1.  In Internet Explorer, navigate to your SharePoint 2010 site.

2.  Navigate to the Shared Documents document library.

3.  Click **Site Actions** \(above the ribbon\), and then click **More Options**.

4.  Select the Web Part page and click **Create**.

5.  Type a name for the new page.

6.  Under **Layout**, select **Header, Right Column, Body** from the list of available layout templates.

7.  Click **Create** to create the new Web page.

8.  Click the Body zone. You should see a new **Insert** tab on the ribbon.

9. On the **Insert** tab, click **Web Part**.

10. In the **Categories** list, click **Office Client Applications**, and then, in the **Web Parts** list, click **Visio Web Access**.

11. Click **Add**.

    The Visio Web Access Web Part is added to the Body zone of the Web part page.

12. Edit the properties of the Visio Web Access Web Part. In the **Web Part** toolbar, click **Edit Web Part**.

13. Set the **Web Drawing URL** property. Click Browse and navigate to the document library where you published a Visio diagram. Select the published diagram and click **OK**.

14. Set the **Automatic Refresh** property to 1 minute \(the minimum value supported\). This enables the dashboard to automatically refresh the diagram with new data from the management server every 1 minute.

15. Clear the **Show Open in Visio** option in the Toolbar and User Interface section.

16. Click **OK** to apply the changes.

    You should now see the rendered Visio diagram in the browser.

17. Click **Stop Editing** to exit edit mode.

Your Web part should now display with the published diagram in the Visio Web Access Web part. Notice that the **Open in Visio** button \(normally available by default\) is no longer available in the Web part toolbar.

