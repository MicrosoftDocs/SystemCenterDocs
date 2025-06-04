---
title: Use SharePoint to View Operations Manager Data
description: This article describes how to deploy the Operations Manager Web console SharePoint web part for viewing select dashboards in SharePoint from Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: d19b28c0-a346-4806-8973-18d5f40ce4fb
---

# Use SharePoint to view Operations Manager data



System Center Operations Manager can display select dashboards from the Web console in SharePoint to see at a glance the status of operational metrics, such as availability and performance of your managed services. This is especially beneficial to members of your organization who don't need access to Operations Manager, such as service managers, executives, and even end-users of the service.  

Use the following procedures to configure dashboards on a SharePoint page. This is accomplished using the Page Viewer Web Part included with SharePoint, which lets you view another web page from within your SharePoint page. If the user hasn't already been granted rights to view operational data from either console available in Operations Manager, they'll need to be [assigned membership](manage-security-overview.md#how-to-assign-members-to-built-in-user-roles) to one of the built-in user roles. If the user will only need to view the data but not interact with it from the Operations or web console, such as close an alert or perform some other related task, consider adding them to the **Read-only Operator** role.

> [!NOTE]
> Silverlight-based dashboards made accessible from the SharePoint web part can only be viewed using the Internet Explorer.

## Configure the web part to connect to a Web console  

1. Open an Internet browser, and then navigate to the SharePoint server.  

2. In the **Site Actions** dropdown menu, select **New Page**.  

3. Enter a name for the page, and select **Create**.  

4. The new page opens with editing tools available. Select **Insert**.  

5. On the **Insert** toolbar, select **Web Part**.  

6. In **Categories**, select **Media and Content** and then select **Page Viewer**. Select **Add** to the page.

7. Select the arrow in the top right of the web part, and select **Edit web part**.  

8. In the **To specify a link, type a URL or path** field, enter the URL of an Operations Manager Web console dashboard view.  

    - For Operations Manager 2016 and URs, append `&disabletree=true` at the end of the URL to disable the tree view from being displayed with the web part.

    - For Operations Manager 2019 and later, and the corresponding URs, append `?removeTree=True` at the end of the URL to disable the tree view from being displayed with the web part.

    To enable the tree view, don't append any value at the end of the URL.

9. Configure the appearance, layout, and Advance properties of the SharePoint page, and select **OK**.

10. On the menu bar, select **Save & Close**.  

## Next steps

- You can use views and dashboards to visualize operational data from different perspectives to make meaningful decisions. To understand how to do this, see [Using Views and Dashboards in Operations Manager](manage-console-using-views-dashboards.md).

- To learn how you can use reports in Operations Manager to view historical operational data, see [Using reports in Operations Manager](manage-reports-installed-during-setup.md).
