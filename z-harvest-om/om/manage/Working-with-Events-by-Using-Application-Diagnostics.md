---
title: Working with Events by Using Application Diagnostics
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caf7af6f-5967-48a0-b0e5-47cb0e0314f7
author:mgoedtel
manager:cfreemanwa
---
# Working with Events by Using Application Diagnostics
Working with alerts is a standard part of working with [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)]. Alerts for .NET application monitoring show you the information you will recognize from other alerts, such as the general information and product knowledge. However, a .NET application alert also provides a link in the alert description. This link opens the event that raised the alert in Application Diagnostics. Here you can see far more information that will help you troubleshoot and identify your problem and solution.  
  
> [!NOTE]  
> Deep troubleshooting of alerts from Application Performance Monitoring often requires access to the application source code and might require input from developers. You can install the Team Foundation Server Work Item Synchronization Management Pack and forward alerts to Team Foundation Server used by the development team. The Team Foundation Server Work Item Synchronization Management Pack tracks and synchronizes changes made to Team Foundation Server work items and changes made to associated Operations Manager alerts.  
  
## Investigating .NET Application Alerts  
Decreasing the time it takes to determine, assign, and resolve issues is the central goal of application monitoring in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)]. When you receive an alert, you need to know what caused it-the system hosting the application or the code, be able to show the data to back up that conclusion, and clearly see who should fix the problem. To know if it is a system issue, you need to know the state of your system at the time of the event. To know where the root problem occurred, you need to know the chain of calls that occurred. To further investigate you need to compare similar events and related events that happened at the same time. Together, the event details, performance counters, and distributed chains will help you triage who should look at this problem first. If it is a system error you can adjust the available resources or configuration of the host system and address the issue at the host level. If it is an application failure, the problem will need to go to the application team along with the line of code where the failure occurred. Here are some strategies for using the views, filters, and settings in Application Diagnostics to help you get to the root cause, find a resolution, and better know who needs to be involved to fix the problem.  
  
#### To open Application Diagnostics from an alert  
  
1.  Since you are responding to alerts related to specific application groups that you configured, it is helpful to scope active alerts and view them by application group. In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, expand **Application Monitoring**, expand **.NET Monitoring**, click the folder with the name of the application group you configured for monitoring whose alerts you want to investigate, and then click **Active Alerts**.  
  
2.  Double\-click the alert you want to open.  
  
3.  On the **Alert Properties** page, click the link in the **Alert Description** pane. This opens Application Diagnostics, a new monitoring feature in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] in a web browser. Here on the **Event properties** tab you can see information, such as the performance metrics, the call stack, and collection notes about the alert. Using the tabs, you can see similar events, related events, event chains, and performance counters. This is detailed information about the performance or exception event that was raised for the application that will help you diagnose whether the issue is coming from the application itself, a call to a web service, or a call to a database. For more information on the Event properties tab, see Performance Event Details. Click **Yes** to close the main window once the event information has loaded.  
  
    > [!NOTE]  
    > This link to Application Diagnostics is also on the on the **Alert Context** tab.  
  
Use the following procedures to investigate your alert. IT Pros will most likely want to use information on the Event properties, Performance counters, and Distributed chains tabs to find out what happened, understand if a system issue caused the problem, and investigate where the root cause occurred. Developers will most likely need to use the information on the Distributed chains, Similar events, and Related events tabs to understand the specific context around a code problem.  
  
#### To troubleshoot by using Exception Event properties in Application Diagnostics  
  
1.  In the Application Diagnostics window for the exception alert you are investigating, click the **Event properties** tab to view key details about the alert. This is the first place to check to see if the alert problem is apparent. Some of the key categories of information you will see on the Event properties page are as follows:  
  
    -   **Source** To display the application load and response times, click the **Source** link in the upper\-left corner. This information shows the load the system was under in the context of the exception event failure. To view performance counters and further assess system state, on the Source page, click the **Trend reports** tab. To see which computers this application is working on and see if there might be a load balancing problem across computers, click the **Computers** tab. To see a breakdown of related calls, or where the events are happening based on chains, click the **Topology** tab.  
  
    -   **Exception Chain** This displays for exception events. Expand Exception Chain to view the actual exception that occurred.  
  
    -   **Exception Data** This displays for exception events and shows parameters and variables set for the class through the exception.  
  
    -   **Stack** This is the call stack, or order in which things happened. The Execution Tree View allows you to expand nodes to investigate the calls. Click the **Resource Group View** radio button to display an overview of where time was spent. This answers which tier the problem is in, or where is it occurring.  
  
    -   **Modules List** This displays for exception events and shows modules loaded at time of exception.  
  
    -   **Collection Notes** This displays any notes about the event.  
  
    > [!TIP]  
    > Use the same troubleshooting steps for Performance events, Similar events, Related events, Distributed chains, and Performance counters as you did for Exception events.  
  
#### To troubleshoot by using Performance Event properties in Application Diagnostics  
  
1.  In the Application Diagnostics window for the performance alert you are investigating, click the **Event properties** tab to view key details about the alert. This is the first place to check to see if the alert problem is apparent. Some of the key categories of information you will see on the Performance properties page are as follows:  
  
    -   **Source** To display the application load and response times, click the **Source** link in the upper\-left corner. This information shows the load the system was under in the context of the exception event failure. To view performance counters and further assess system state, on the Source page, click the **Trend reports** tab. To see which computers this application is working on and see if there might be a load balancing problem across computers, click the **Computers** tab. To see a breakdown of related calls, or where the events are happening based on chains, click the **Topology** tab.  
  
    -   **Slowest Nodes** This is a list of the slowest nodes in the Execution Tree View and the most likely cause of the performance issues in the application.  
  
    -   **Stack** This is the call stack, or order in which things happened. The Execution Tree View allows you to expand nodes to investigate the calls. Click the **Resource Group View** radio button to display an overview of where time was spent. This answers which tier the problem is in-where is it occurring?  
  
    -   **Collection Notes** This displays any notes about the event.  
  
#### To troubleshoot the state of the system by using Performance counters  
  
1.  To view a table or diagram of key performance counters, click the **Performance counters** tab.  
  
    > [!NOTE]  
    > Fifteen minutes of performance data is collected and cached on the monitored system. When a performance or exception is raised, the performance data is sent back to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] along with the event.  
  
2.  Select the performance counter checkboxes for the performance counters you want to include in your information, and then click **Apply**.  
  
3.  Use the information in this display to assess the system performance state around the event you are investigating.  For example, if the performance is uniformly slow at the time of the event, then your alert is likely due to a system performance problem.  
  
#### To find the root problem by using Distributed chains  
  
1.  Click the **Distributed chains** tab to view the order of calls-the chain of events of which the event is part. This helps you understand how the event you are investigating was impacted by other events from the application or related applications.  
  
2.  In the Distributed chains view, click one of the calls, or links, in the chain. If there are multiple events for the same object, the Chaining Wizard will open. This wizard allows you to select possible events to correlate into a chain of events. To begin the Wizard, click **Next**.  
  
    > [!NOTE]  
    > Get the time stamp from the call you select as you will pair this with an event on the next page.  
  
3.  The **Select Possible Chain Event** page, select the event that you want to examine. Ideally it will be the event with the time stamp that is closest to call you selected in the Distributed Chains view.  
  
4.  What you see next depends on the kind of problem you are investigating. For example, if you select a transaction where a server is not found, you might go to the event properties page for that event. This will let you pair the server error with the event you were initially investigating. Since it is a server error, you know that the problem is not on the client side, but server side. You might see a graph of the event you selected and be able to breakdown a performance event in terms of the page load time.  
  
5.  From event properties, click the server\-side call, and click the **Performance Counters** tab for more details.  
  
#### To troubleshoot by viewing similar events  
  
1.  Click the **Similar events** tab to see if similar alerts have been thrown more times, which could mean that there is a problem with the application.  
  
2.  There are several ways to filter similar events. Click the **Similar by** dropdown menu to select how you want to group the similar events: by problem, action, exception class, or failed function. In the **From** and **To** text boxes, you can set the range of dates from which you want to view the similar events. Use the **Similar events** tab to view if similar alerts has been thrown more times, which could mean that there is a problem with the application.  
  
    -   **Filtering by Problem** shows you similar events that are of the same type. For example you can see all similar events where the object reference is not set to an instance of an object. Click the **Diagram View** button and you can see the ratio of total number of events for the current problem and the total number of events from other problems. This information gives you a quick view into the magnitude of the problem that this particular event has. If many of the current total similar events have the same problem, it might be a higher priority problem to resolve since it will have high impact in reducing the number of alerts you receive.  
  
    -   **Filtering by Action** groups the similar events by aspect: security, performance, connectivity, and application failure. Click the **Diagram View** button and you can see the number of similar events by these aspect categories and more easily see which ones the problem might be related to.  
  
    -   **Filtering by Exception class** groups the similar events according to how you named them during configuration. Presumably, these would be names that would help you identify the kind of exceptions they are, such as **System.NullReferenceException** class.  
  
    -   **Filtering by Failed function** groups the similar events by the same function is throwing the exception. This could mean that there is a problem with the entry point.  
  
    Keep in mind that these are all similar events-related by definition-and these filters give you a better idea of exactly how they are related. So, using the Similar Events filters, you might find that most of your total events have the same problem as the event you are viewing, that it is a performance problem, that they belong to an exception class you configured, and that half of the similar events had the same failed function. Action: The function goes to the developer who needs to update the function code.  
  
#### To troubleshoot by viewing related events  
  
1.  Click the **Related events** tab to view events that are related by time. These are exceptions correlated with other events that might give you an insight to the problem.  
  
2.  To view the event details of an event in the list, click the link in the **Description** column.  
  
    In the related events you might notice that response time is very slow for all events during a certain time. This could indicate a problem with the system, not the code, and so might go to the IT pro for a solution.  
  
