---
title: Prioritizing Alerts by Using Application Advisor
description: This article describes how to use Application Advisor to identify exceptions detected from your monitored web application.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 06/06/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
ms.assetid: a9d0f6f6-90df-4159-9a24-5ba0647a2343
---

# Prioritizing alerts by using Application Advisor
Application Advisor works with .NET Application Performance Monitoring in System Center 2016 - Operations Manager and helps you prioritize and manage which alerts to address. It identifies which applications are causing the most alerts within an environment. These are the applications you should investigate first because they are causing the most service level agreement (SLA) violations. Use Application Advisor as a first step in alert management and as a view into the overall health of an application. Essentially, Application Advisor helps you "follow the noise" and find out where the most events are occurring. Application failure and analysis reports let you view those individual applications in fine detail. Summary reports give you key information at a glance, such as the top-five alerts to resolve.  
  
### Scope and run an Application Advisor report  
  
1.  Application Advisor and Application Diagnostics are installed along with the Operations Manager web console. To find the web address of the Operations Manager web console, open the Operations console. In the navigation pane, select **Administration**, click **Settings**, and then double-click **Web Addresses**. The Operations Manager web console URL will be specified as: `http(s)://<web host>/OperationsManager`. Using this URL format and the same web host, here are the links to Application Advisor and Application Diagnostics:  
  
    -   The Application Advisor console address is:` http(s)://<web host>/AppAdvisor`  
  
    -   The Application Diagnostics console address is: `http(s)://<web host>/AppDiagnostics`  
  
    To make access easy, add all three console URLs to your web browser's favorites list.  
  
    To open Application Advisor, paste the Application Advisor URL into your browser. Application Advisor opens in the web browser window. Different application monitoring reports display in the context of the application features and services you configured when you created application groups to monitor.  
  
    Access to Application Advisor is controlled through the Application Monitoring Operator, Report Operator and Administrator roles. You must be a member of Application Monitoring Operator and Report Operator roles or the Administrator role. For more information, see [User roles for Application Performance Monitoring](manage-working-with-the-application-diagnostics-console.md#user-roles-for-application-performance-monitoring). 
  
    Access to Application Diagnostics is controlled through the Application Monitoring Operator and Administrator roles. You must be a member of one of these roles to have rights to the console.  
  
    > [!NOTE]  
    > Application Advisor requires SQL Server Report Services (SSRS). You must have Operations Manager Reporting server installed before using Application Advisor.  
  
2.  In the **Navigation** pane, in the **All application groups** dropdown menu, select whether you want reports to include information for all application groups or a subset of application groups.  
  
    > [!NOTE]  
    > Application groups are created in the Application Diagnostics console. Use them to create a group of applications to which you would like to scope your reports. Using many application groups can have a performance impact.  
  
3.  In the **Select report** menu, select how you want to scope the reports, and then click the report you want to run. You can scope reports by Client-Side Monitoring, Problem Analysis Reports, Resource Utilization analysis, or choose just one of the individual reports to view.  
  
    You can also select a report by clicking on one of the report graphics.  
  
4.  Use the **Start Date** and **End Date** fields to select the time or date range for the alerts you want included in the reports.  
  
5.  Click the **Status** text box to filter alerts by those that are New, Reviewed, Deleted, or By Design.  
  
    > [!TIP]  
    > Viewing alerts categorized as By Design can show you if the way an application is designed is actually causing issues.  
  
6.  Click **Source** dropdown menu to select the application component you want to include in the report.  
  
    > [!NOTE]  
    > Only applications that are part of the application group you initially selected are available to be used as a source.  
  
7.  Click the **Computer** dropdown menu to select which computer or computers you want reported on.  
  
8.  In the **Problem** dropdown menu, you can filter by all problems detected or only critical problems.  
  
9. Click **Apply** to save this report configuration and run the report.  
  
## Example: To Prioritize Alerts by Using the Problems Distribution Analysis Report  
A first step in working with application monitoring alerts is to try to see which ones you should address first to have the greatest impact on the applications in your environment. This is the role of Application Advisor - to identify the applications causing the most alerts and to see the types of alerts being raised. This introduces a proactive approach to managing application health because you are smartly addressing the most problematic areas of your applications and not merely reacting to alerts as they arrive.  
  
To show how Application Advisor prioritizes alerts, this walkthrough uses a report that is helpful when first investigating application issues: the Problems Distribution Analysis report. This report shows the distribution of application failure, performance, connectivity, and security problems across all monitored applications-and highlights the applications that are the most problematic. For the applications that contributed to the majority of problems, this report provides more details by showing application components and external dependencies that are the root cause of those problems.  
  
### Interpret key elements of the Problems Distribution Analysis Report  
  
1.  Following the procedure to scope and run an Application Advisor report, choose the information you want to include in the report, and then click **Apply** to run the report.  
  
2.  Here there are three views that will show top issues:  
  
    -   To view only performance problems and top performance events for the applications, click **Summary Performance Analysis**.  
  
    -   To view only exceptions and top exception events for the applications, click the **Summary Failure Analysis** link.  
  
    -   You can view all problem types and top problems for the individual application, in the **Overall Source Statistics** section. This section shows you what percentage of performance and exception events are being raised by the application resources, such as function calls or database queries.  
  
3.  Click the first link in whichever view you want to investigate. This first link shows the highest cause of alerts and launches a list of all problems related to that application or source.  
  
    > [!IMPORTANT]  
    > This is the stage where you shift from a prioritized list to investigating individual alerts related to the most important issue. None of the events in this list is more important than another, but each can help highlight the route cause.  
  
4.  Click a link in **Event Description** and the Application Diagnostics Event Properties page opens. Here you are viewing data about the event itself. And this is the place to start troubleshooting. See [Working with events by using Application Diagnostics](manage-working-with-events-using-application-diagnostics.md) for more information.  
  
    Beginning with Event properties tab, use this and other tabs to discover more about what happened, whether it was likely a system issue as shown by performance data, and what application tier the problem occurred in, using distributed chains. Following this information should reveal if it was a system problem or an application code problem, and thus who should resolve the issue.  
  
## Add an Application Advisor report to Favorites  
  
1.  If you want to save a report with certain scoped information that you can easily view later, add it to your Favorites list. In the **Select report** menu or by clicking the report graphic, select the report you want to run.  
  
    > [!NOTE]  
    > You can scope the information you want included in the report before making it a favorite or create the scoping information in the Favorite Management Wizard.  
  
2.  In the **Results** pane, to open the Favorite Management Wizard, click the Favorites icon.  
  
3.  In the Favorite Management Wizard, you can either keep the settings you used to scope the information to be included in your report, reset them, or set them for the first time.  
  
4.  As you make or confirm your scoping settings, click **Next** to proceed through the wizard settings pages, and then click **Finish**.  
  
5.  In the Favorites namespace, click **Favorites** and you will be able to view the report you just configured.  
  
6.  To view a report in your Favorites, just click the report you want to view.  
  
## Next steps

  
