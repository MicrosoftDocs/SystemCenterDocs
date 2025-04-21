---
title: Prioritize Alerts by Using Application Advisor
description: This article describes how to use Application Advisor to identify exceptions detected from your monitored web application.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/21/2025
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: a9d0f6f6-90df-4159-9a24-5ba0647a2343
---

# Prioritize alerts by using Application Advisor

This article describes how to use Application Advisor to identify exceptions detected from your monitored web application.

Application Advisor works with .NET Application Performance Monitoring in System Center - Operations Manager and helps you prioritize and manage which alerts to address. It identifies which applications are causing the most alerts within an environment. These are the applications you should investigate first because they're causing the most service level agreement (SLA) violations. Use Application Advisor as a first step in alert management and as a view into the overall health of an application. Application Advisor helps you **follow the noise** and find out where the most events are occurring. Application failure and analysis reports let you view those individual applications in fine detail. Summary reports give you key information at a glance, such as the top five alerts to resolve.  

### Scope and run an Application Advisor report  

To scope and run an Application Advisor report, follow these steps:

1.  Application Advisor and Application Diagnostics are installed along with the Operations Manager web console. To find the web address of the Operations Manager web console, open the Operations console. In the navigation pane, select **Administration**, select **Settings**, and then double-click **Web Addresses**. The Operations Manager web console URL will be specified as: `http(s)://<web host>/OperationsManager`. Using this URL format and the same web host, here are the links to Application Advisor and Application Diagnostics:  

    -   The Application Advisor console address is:` http(s)://<web host>/AppAdvisor`  

    -   The Application Diagnostics console address is: `http(s)://<web host>/AppDiagnostics`  

    To make access easy, add all three console URLs to your web browser's favorites list.  

    To open Application Advisor, paste the Application Advisor URL into your browser. Application Advisor opens in the web browser window. Different application monitoring reports display in the context of the application features and services you configured when you created application groups to monitor.  

    Access to Application Advisor is controlled through the Application Monitoring Operator, Report Operator, and Administrator roles. You must be a member of Application Monitoring Operator and Report Operator roles or the Administrator role. For more information, see [User roles for Application Performance Monitoring](manage-working-with-the-application-diagnostics-console.md#user-roles-for-application-performance-monitoring).

    Access to Application Diagnostics is controlled through the Application Monitoring Operator and Administrator roles. You must be a member of one of these roles to have rights to the console.  

    > [!NOTE]  
    > Application Advisor requires SQL Server Report Services (SSRS). You must have Operations Manager Reporting server installed before using Application Advisor.  

2.  In the **Navigation** pane, in the **All application groups** dropdown menu, select whether you want reports to include information for all application groups or a subset of application groups.  

    > [!NOTE]  
    > Application groups are created in the Application Diagnostics console. Use them to create a group of applications to which you would like to scope your reports. Using many application groups can have a performance impact.  

3.  In the **Select report** menu, select how you want to scope the reports, and then select the report you want to run. You can scope reports by Client-Side Monitoring, Problem Analysis Reports, Resource Utilization analysis, or choose just one of the individual reports to view.  

    You can also select a report by clicking on one of the report graphics.  

4.  Use the **Start Date** and **End Date** fields to select the time or date range for the alerts you want included in the reports.  

5.  Select the **Status** text box to filter alerts by those that are New, Reviewed, Deleted, or By Design.  

    > [!TIP]  
    > Viewing alerts categorized as By Design can show you if the way an application is designed is actually causing issues.  

6.  Select the **Source** dropdown menu to select the application component you want to include in the report.  

    > [!NOTE]  
    > Only applications that are part of the application group you initially selected are available to be used as a source.  

7.  Select the **Computer** dropdown menu to select which computer or computers you want reported on.  

8.  In the **Problem** dropdown menu, you can filter by all problems detected or only critical problems.  

9. Select **Apply** to save this report configuration and run the report.  

## Example: To prioritize alerts by using the Problems Distribution Analysis Report  

A first step in working with application monitoring alerts is to try to see which ones you should address first to have the greatest impact on the applications in your environment. This is the role of Application Advisor - to identify the applications causing the most alerts and to see the types of alerts being raised. This introduces a proactive approach to managing application health because you're smartly addressing the most problematic areas of your applications and not merely reacting to alerts as they arrive.  

To show how Application Advisor prioritizes alerts, this walkthrough uses a report that's helpful when first investigating application issues: the Problems Distribution Analysis report. This report shows the distribution of application failure, performance, connectivity, and security problems across all monitored applications and highlights the applications that are the most problematic. For the applications that contributed to most of the problems, this report provides more details by showing application components and external dependencies that are the root cause of those problems.  

### Interpret key elements of the Problems Distribution Analysis Report  

To interpret key elements of the Problems Distribution Analysis Report, follow these steps:

1.  Following the procedure to scope and run an Application Advisor report, choose the information you want to include in the report, and select **Apply** to run the report.  

2.  Here there are three views that will show the top issues:  

    -   To view only performance problems and top performance events for the applications, select **Summary Performance Analysis**.  

    -   To view only exceptions and top exception events for the applications, select the **Summary Failure Analysis** link.  

    -   You can view all problem types and top problems for the individual application in the **Overall Source Statistics** section. This section shows you what percentage of performance and exception events are being raised by the application resources, such as function calls or database queries.  

3.  Select the first link in whichever view you want to investigate. This first link shows the highest cause of alerts and launches a list of all the problems related to that application or source.  

    > [!IMPORTANT]  
    > This is the stage where you shift from a prioritized list to investigating individual alerts related to the most important issue. None of the events in this list is more important than another, but each can help highlight the root cause.  

4.  Select a link in **Event Description**, and the Application Diagnostics Event Properties page opens. Here you're viewing data about the event itself. And this is the place to start troubleshooting. For more information, see [Work with events by using Application Diagnostics](manage-working-with-events-using-application-diagnostics.md).  

    Beginning with the Event properties tab, use this and other tabs to discover more about what happened, whether it was likely a system issue as shown by performance data, and what application tier the problem occurred in, using distributed chains. Following this information should reveal if it was a system problem or an application code problem, and thus who should resolve the issue.  

## Add an Application Advisor report to Favorites 

To add an Application Advisor report to Favorites, follow these steps:

1.  If you want to save a report with certain scoped information that you can easily view later, add it to your Favorites list. In the **Select report** menu or by clicking the report graphic, select the report you want to run.  

    > [!NOTE]  
    > You can scope the information you want included in the report before making it a favorite or create the scoping information in the Favorite Management Wizard.  

2.  In the **Results** pane, to open the Favorite Management Wizard, select the Favorites icon.  

3.  In the Favorite Management Wizard, you can either keep the settings you used to scope the information to be included in your report, reset them, or set them for the first time.  

4.  As you make or confirm your scoping settings, select **Next** to proceed through the wizard settings pages, and select **Finish**.  

5.  In the Favorites namespace, select **Favorites** and you'll be able to view the report you just configured.  

6.  To view a report in your Favorites, select the report you want to view.  

## Next steps

To understand how to work with sensitive data that would be collected and be available for viewing by Application Performance Monitoring, review [Work with sensitive data for .NET applications](manage-working-with-sensitive-data-dotnetapps.md).  
