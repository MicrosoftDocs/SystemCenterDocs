---
title: Work with the Application Diagnostics Console
description: This article describes how to use the Application Diagnostics console to review captured application error, exceptions, and events.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/21/2025
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: bb451d4a-4e48-428d-8992-0f2e2b5c240f
---

# Work with the Application Diagnostics console



The Application Diagnostics console is an event management system for .NET Application Performance Monitoring in System Center - Operations Manager. You can use Application Diagnostics console to monitor deployed .NET applications for slowdowns, faults, and failures, and immediately pinpoint the source of the problem.  

This article describes how to use the Application Diagnostics console to review captured application error, exceptions, and events.

## User roles for Application Performance Monitoring

The following table shows the Operations Manager .NET Application Performance Monitoring tasks and the user roles with their permissions.  

Legend:  

*  Yes - Can always use the feature  

*  No - Can't use the feature unless the user also belongs to a group that grants access to this functionality  

|Tasks|Administrator|Author|Advanced Operator|Application Monitoring Operator|Operator|Read-Only Operator|Report Operator|Report Security Administrator|  
|-|-----------------|----------|---------------------|-----------------------------------|------------|-----------------------|-------------------|---------------------------------|  
|Run APM Wizard or change APM settings|Yes|No|No|No|No|No|No|No|  
|Access Application Diagnostics|Yes|No|No|Yes|No|No|No|No|  
|Access Application Advisor|Yes|No|No|Yes\*|No|No|Yes\*|Yes|  

> [!NOTE]  
> \* The Application Monitoring Operator role and Report Operator role are both required to access Application Advisor.  


## The Application Diagnostics console  
The Application Diagnostics console is the place to look at the individual performance and reliability events that are being raised within your environment. You can look at all the events, or group them into "problem groups" in which events coming from the same sources are grouped together to highlight the problems with the monitored applications. Use Application Diagnostics to look at events and the transaction chains related to those events to understand how the performance and reliability issues are affecting your applications. 

The Application Advisor console provides analytics and telemetry of the data presented in Application Diagnostics. Through the Application Advisor console you gain insights into which events are causing the most problems. For more information about Application Advisor, see [Prioritize alerts by using Application Advisor](manage-prioritizing-alerts-using-application-advisor.md)  


### Open the Application Diagnostics console  

Application Diagnostics and Application Advisor are installed along with the Operations Manager web console. To find the web address of the Operations Manager web console, open the Operations console. In the navigation pane, select **Administration**, select **Settings**, and then double-click **Web Addresses**. The Operations Manager web console URL will be specified as: `http(s)://<web host>/OperationsManager`. Using this URL format and the same web host, here are the links to Application Advisor and Application Diagnostics:   

- The Application Diagnostics console address is: `http(s)://<web host>/AppDiagnostics`  

- The Application Advisor console address is: `http(s)://<web host>/AppAdvisor`  

To make access to the consoles easy, add all three console URLs to your web browser's favorites list.  

To open Application Diagnostics, paste the Application Diagnostics URL into your browser. Application Diagnostics opens in the web browser window.  

> [!NOTE]  
> If you're running Operations Manager on a server rather than a client computer, you can access Application Diagnostics and Application Advisor from the **Start** menu.  

Access to Application Diagnostics is controlled through the Application Monitoring Operator and Administrator roles. You must be a member of one of these roles to have rights to the console.

## View Events by Areas of Interest  

In Application Diagnostics, there are two major types of events: those related to application performance and those related to application failures and errors. The failures and errors can be divided further into connectivity, security, and failure issues. Failure issues are typically related to a problem with the application code. In Application Diagnostics, you can view events grouped in these ways:  

-   All (displays all events)

-   Application Errors (displays exception events) 

-   Performance (displays performance events) 

To view Events by Areas of Interest, follow these steps:

1.  Open Application Diagnostics and select **Events** from the Navigation pane.  

2.  In the Navigation pane, use the **Search for** menu to select the category of events you want to view.  

## Group Events within Areas of Interest  

Grouping application events by similarity provides the best method for determining if the same issue has occurred before and ensuring that resources responsible for the issue resolution are allocated in the most efficient way.

To group Events within Areas of Interest, follow these steps:

1.  Open Application Diagnostics, and select **Events** from the Navigation pane.  

2.  In the Navigation pane, use the **Search for** menu to select the category of events you want to view.  

3.  In the **Group By** menu, select the way you want to group the events.  

Your first selection (**Application Errors** and **Performance**) affects the grouping options you see for your second selection.  

### Group Application Errors

-   **Problem** What it displays: All events in this grouping are coming from the same entry point into the application (for example, a method or a web page) and have the same call stack. Value: Consolidating events by problem allows you to prioritize your efforts to correct an issue based on the number of events in the group.  

-   **Action** What it displays: Action-based consolidation categorizes events based on entry points, such as page calls, button clicks, web service calls, or some other action representing a particular process. Value: This grouping is valuable for determining under what circumstances a failure occurs.  

-   **Exception Class** What it displays: The bottom level exception thrown by each event is the same. Value: Consolidating by exception class is a good way to find the most typical coding mistakes and promotes improved coding practices.  

-   **Failed Function** What it displays: The exception occurred in the same function for each event. Value: This grouping is valuable for two reasons: First, it allows you to identify cases where a shared function is used incorrectly. Second, it allows you to identify how many applications are affected by an error in a shared function.  

-   **None** This option doesn't group the events.  

### Group Performance Events

-   **Problem** What it displays: All events in this grouping have the identical call stack. Value: Consolidating events by problem allows you to prioritize your efforts to correct an issue based on the number of events in the group.  

-   **Heaviest Resource** What it displays: All events triggered by the same resource call. This grouping is valuable for determining which events exceeded their thresholds more than the other resources.  

-   **None** This option doesn't group the events.  



## [Example: Grouping Application Errors by Exception Class](#tab/example-grouping-application-errors-by-exception-class)  

Filtering by application errors and exception class quickly shows you which kinds, or classes, of exception events you're receiving most often.  

![Screenshot showing Filter by application errors and exception class.](./media/om2016-appmonitoring-appdiagnosticsfilter-excepterror.png)  

To filter by application errors and exception class, follow these steps:


1.  Open Application Diagnostics and select **Events** from the Navigation pane.  

2.  In the Navigation pane, in the **Search for** menu, select **Application Errors**.  

3.  In the **Group By** menu, select **Exception Class**.  

4.  To sort by count, at the top of the Count column, select **Count**. The exception classes that have occurred most often are ranked from the highest to the lowest.  

5.  To begin investigating the issue and open Event properties, select an **Exception Class** entry. For information about working with events, see [Work with events by using Application Diagnostics](manage-working-with-events-using-application-diagnostics.md).

## [Example: Grouping Application Errors by Failed Function](#tab/example-grouping-application-errors-by-failed-function)  

Filtering by application errors and failed function quickly shows you which functions are failing most often. The functions that are failing the most are the ones you should investigate first to have the highest impact on your application's reliability.  

![Screenshot showing Filter by application errors and failed function.](./media/om2016-appmonitoring-appdiagnostics-filtererrorsfailedfunct.png)  

To filter by application errors and failed function, follow these steps:

1.  In the navigation pane, in the **Search for** menu, select **Application Errors**.  

2.  In the **Group By** menu, select **Failed Function**.  

3.  To sort by count, at the top of the Count column, select **Count**. The functions that have failed most often are ranked from the highest to the lowest.  

4.  To begin investigating the issue and open Event properties, select a **Failed Function** entry. For information about working with events, see [Work with events by using Application Diagnostics](manage-working-with-events-using-application-diagnostics.md).

## [Example: Grouping Performance Events by Heaviest Resource](#tab/example-grouping-performance-events-by-heaviest-resource)  

Filtering by application errors and exception class quickly shows you which performance events are triggered by the same resource call. The performance events that are most often triggered by the same resource call are the ones you should investigate first to have the highest impact on your application's performance.  

![Screenshot showing Filter by performance and heaviest resource.](./media/om2016-appmonitoring-appdiagnosticsfilter-heavyres.png)  

To filter by application errors and failed function, follow these steps: 

1.  In the navigation pane on the left, in the **Search for** menu, select **Performance**.  

2.  In the **Group By** menu, select **Heaviest Resource**.  

3.  To sort by count, at the top of the Count column, select **Count**. The exception classes that have occurred most often are ranked from the highest to the lowest. You can also sort by average duration and maximum duration to see if some events that are occurring less often are still causing long delays and should therefore receive your attention.  

4.  To begin investigating the issue and open Event properties, select a **Heaviest Resource** entry. For information about working with events, see [Work with events by using Application Diagnostics](manage-working-with-events-using-application-diagnostics.md).

---

## Next steps

* To learn how to prioritize and manage which alerts to address and where the most events are occurring, review [Prioritize alerts by using Application Advisor](manage-prioritizing-alerts-using-application-advisor.md).  

* To learn how to view alerts and begin investigating the issues raised, review [View and investigate alerts for .NET applications](manage-viewing-and-investigating-alerts-for-dotnetapps.md).
