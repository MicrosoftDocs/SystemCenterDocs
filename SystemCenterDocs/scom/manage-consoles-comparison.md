---
title: Compare the Operations and Web Console
description: This article describes both of the Operations Manager consoles and the differences between them for viewing monitoring data and performing administration in the management group.
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.date: 02/04/2026
ms.custom: UpdateFrequency2, engagement-fy24
ms.update-cycle: 1095-days
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 10d18a5f-c45d-4c23-b77e-b1cfbde31572
---

# Compare the Operations and Web consoles

System Center Operations Manager includes two consoles:

- The Operations console
- The Web console

Use the Operations console as the primary tool for managing your Operations Manager deployment. In the Operations console, you can view and interact with alerts and monitoring data, manage and edit monitoring configuration, generate and view reports, administer management group settings, and build a personal workspace that's customized to your needs.

The Web console is a web-based user interface that provides access to all the monitoring data and tasks that you can run against monitored computers from the Operations console. It doesn't have the full functionality of the Operations console and provides access to only the Monitoring and My Workspace views.

Both consoles share a similar layout:  

:::image type="content" source="./media/manage-consoles-comparison/om2016-consoleframe.png" alt-text="Diagram of the console panes.":::

Each navigation button opens a specific workspace, such as Monitoring or Administration. In the Operations console, the following navigation buttons are available depending on the user role you're assigned:  

:::image type="content" source="./media/manage-consoles-comparison/om2016-operations-console-navbuttons.png" alt-text="Screenshot of the Navigation buttons in Operations Console.":::

In the Web console, only Monitoring and My Workspace are available:  

:::image type="content" source="./media/manage-consoles-comparison/om2016-web-console-navbuttons.png" alt-text="Screenshot of the Navigation buttons in Web console.":::

> [!TIP]  
> In the Operations console, you can change the navigation buttons into small icons and increase the space available in the navigation pane by clicking on the top border of the navigation buttons and dragging downward. You can also hide and reveal the navigation and task panes.  

Be aware of a few differences between the Operations console and Web console:  

- There are minor differences in sort. For example, in the Web console, when you sort alerts, only the alerts visible on the page are sorted rather than all alerts.  

- Fewer alerts display per page in the Web console.  

- You can't run tasks that require elevated access in the Web console.  

- You can't access event views.

- Informational alerts don't appear in an alerts view.  

- You don't have the options to show, hide, personalize, or create views in the Web console, although you can create a dashboard view in My Workspace in the Web console.  

- There are no subscription options in the Web console.

## Next steps

* To access and interact with the operational data or perform administrative tasks, see [How to Connect to the Operations and Web Console](manage-consoles-how-to-connect.md).  

* Learn what actions you can perform in the [Monitoring workspace](manage-using-monitoring-workspace.md), [Authoring workspace](manage-using-authoring-workspace.md), [Administration workspace](manage-using-admin-workspace.md), and [Reporting workspace](manage-using-reporting-workspace.md).
