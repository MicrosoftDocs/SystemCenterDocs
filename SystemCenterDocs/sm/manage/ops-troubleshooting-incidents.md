---
title: Troubleshoot incidents
description: Describes how to troubleshoot Service Manager incidents.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44090039-636d-4ab2-bed7-b2196397d781
---

# Troubleshoot Service Manager incidents

>Applies To: System Center 2016 - Service Manager

You can use the following procedures to troubleshoot an incident in Service Manager using a service map. A service map is a visual representation of a service from the perspective of the business and user that shows critical dependencies, settings, and areas of responsibility. Because a service map can show the relationship between incidents and configuration items, it is especially useful when you troubleshoot issues that might affect multiple incidents and configuration items. For example, if an incident affects one configuration item, other configuration items that are part of the service might also be affected. If necessary, you can add additional configuration items as items that are affected by the same open incident.  

 Additionally, when you use the **Service Components** tab to view the service map, you can easily determine whether there are active incidents or change requests open for a service component. When any incidents affect a service component, that component is marked with an orange icon resembling a square containing an exclamation point. When a change request affects a service component, the component is marked with a special blue icon resembling a square containing a right\-pointing arrow.  

### To view incidents that affect service components  

1.  In the Service Manager console, click **Configuration Items**.  

2.  In the **Configuration Items** pane, expand **Business Services**, and then click **All Business Services**.  

3.  In the **All Business Services** list, double\-click a business service. For example, double\-click **Exchange Service**.  

4.  In the dialog box that opens, click the **Service Components** tab.  

     Note that the list of service components includes configuration items. For example, the list might include computers running Microsoft Exchange&nbsp;Server. When a service component is marked with an icon, the icon indicates that an incident is associated with the service component.  

5.  Select a configuration item that has a related work item. For example, select the **Exchange01.woodgrove.com** server.  

6.  In the **Related work items for the selected item** list, select a work item to view, and then click **Open**.  

### To add related service components to an open incident  

1.  In the list of service components, select an item that has an active incident.  

2.  Under **Related work items for the selected item**, select a work item, and then click **Open** to open the incident.  

3.  Under **Affected Items**, click **Add**.  

4.  In the **Select objects** dialog box, select the configuration item to add to the incident, click **Add**, and then click **OK**.  

5.  Click **OK** to update the incident, and then return to the **Service Components** tab for the service.  

6.  Repeat the previous steps to add other service components to the open incident.  

7.  Click **OK** to close the service item.  

### To validate that the service components were added to an incident  

-   Open the business service to which you added the incident, and then click the **Related Items** tab. Verify that the new incident appears under **Work items affecting this configuration item**.  
