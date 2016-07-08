---
title: Dashboard Views for Web Application Availability Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8605ec58-9fef-4715-9f74-a195eefb82c3
author:markgalioto
---
# Dashboard Views for Web Application Availability Monitoring
Dashboards show your test results so you can more effectively see trends and isolate problems for certain tests, locations, and applications.  
  
## Viewing the Dashboards  
To view the Web Application Availability Monitoring dashboards for internal URL tests, you need to use [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] script.  
  
#### To view the Summary and Details dashboards  
  
1.  From the **Start** menu, open the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] Shell.  
  
2.  Use New\-SCOMLocation, Get\-SCOMAgent, and Set\-SCOMLocation to add a location, get an [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agent, and then associate the location with the agent. Here is an example using Seattle, WA as a location:  
  
    ```  
    PS C:\> $Location = New-SCOMLocation -DisplayName “Seattle, WA” -Latitude 47.6063889 -Longitude -122.330833  
    PS C:\> $Agent = Get-SCOMAgent -Name “Server01.Contoso.com”   
    PS C:\> Set-SCOMLocation -Location $Location -Agent $Agent  
    ```  
  
    For more information about adding a location, see [New\-SCOMLocation](http://go.microsoft.com/fwlink/?LinkId=235473). For more information about getting an [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agent, see [Get\-SCOMAgent](http://go.microsoft.com/fwlink/?LinkID=187686). For more information about associating a location with an agent, see [Set\-SCOMLocation](http://go.microsoft.com/fwlink/?LinkId=235479).  
  
3.  After you run the commands, in the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, and then click **Application Monitoring**.  
  
4.  Expand **Web Application Availability Monitoring**, click **Active Alerts**, **Test State**, or **Web Application Status** to display alerts or status for the category.  
  
5.  From any of these views \(alert, test state or web application\), click to highlight the application you want to see a summary of and follow the procedure to view the dashboards in this topic.  
  
## The Summary Dashboard  
If you want to check to see if an application is available, the Summary Dashboard is a helpful view. It displays a world map, the locations you are monitoring from, and the rollup test status from each location. You can then click the location or select several locations to compare.  
  
#### To check the overall status of a web application using the Summary Dashboard  
  
1.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, and then click **Application Monitoring**.  
  
2.  Expand **Web Application Availability Monitoring**, and then click **Active Alerts**, **Test State**, or **Web Application Status** to display alerts or status for the category.  
  
    -   **Active Alerts** displays all alerts for all web applications \(templates\) or tests.  
  
    -   **Test State** displays the state of each test, which is based on how you configured the tests. You can click State, Display Name, and Context column headings to sort the test state list accordingly. For example, if you sort by Context, this groups the list by web applications, so you can see the state of the tests for each web application.  
  
    -   **Web Application Status** displays the worst rollup of tests for each web application. This is a quick way to check whether an application is having any issues.  
  
3.  From any of these views \(alert, test state or web application\), click to highlight an entry for the application you want to see a summary of. Then, in the **Tasks** pane, in the **Navigation** section, click **Summary Dashboard**. This displays a dashboard for the entire application—a world map that shows all locations the application is being tested from and the worst rollup status of all of the tests from each location. For example, red means that at least one test from that location has failed and green means that no tests have failed.  
  
4.  To see the test status for all tests from a given location, click that location and the test status displays below.  
  
5.  If you want to investigate a particular test, or group of tests, click to highlight the tests you want to investigate and in the **Tasks** pane, in the **Navigation** section, click **Detailed Dashboard – List**. This opens detailed views into the item you clicked. For more information, see the details dashboard section below.  
  
## The Details Dashboard  
If you want to investigate a particular test or alert, use the Detailed Dashboard – List. For each web application, you choose the location and which tests in that location you want to investigate. Six key metrics are shown, which you can use to pinpoint and isolate issues and compare the performance of pages from your web applications or compare your pages to competitors’ pages.  
  
#### To pinpoint problems using the Details Dashboard  
  
1.  Begin the same way you opened the Summary Dashboard. In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, and then click **Application Monitoring**.  
  
2.  Expand **Web Application Availability Monitoring**, and then click **Active Alerts**, **Test State**, or **Web Application Status** to display alerts or status for the category.  
  
3.  From any of these views \(alert, test state or web application\), click to highlight the application you want to see a summary of, and in the **Tasks** pane, in the **Navigation** section, click **Detailed Dashboard \- List**.  
  
    > [!TIP]  
    > If you are already viewing the Summary Dashboard, you can go directly to the Detailed Dashboard by clicking to highlight a test or group of tests and then in the **Tasks** pane, in the **Navigation** section, clicking **Detailed Dashboard**.  
  
4.  In the section with the name of your application, for example **Bing template** select the locations you want to see more details about.  
  
5.  In the **Test Status** section, the check boxes act as a legend for the tests you want to investigate in the performance graphs. For example, you can select the same page being tested from different locations to see how the pages are performing for the different locations. Selection \(blue highlighting\) determines which tasks are available and can be run.  
  
## Health Explorer  
As its name implies, Health Explorer allows you to see more details about the health status of a web application availability test running against a URL from a particular location. Health Explorer shows you when a test changed state from, for example, healthy to unhealthy.  
  
#### To view the context of a problem using Health Explorer  
  
1.  To open Health Explorer for a particular test, highlight an alert, test state, or web application status item, and in the **Tasks** pane, click **Health Explorer**. If you are already in a dashboard view, you can also open Health Explorer in the Summary Dashboard and Detailed Dashboard by right\-clicking an entry, and then clicking **Health Explorer**.  
  
2.  In **Health Explorer**, in the pane named with your test, click to highlight an item you want to investigate.  
  
3.  Click the **State Change Events** tab to see details on when a state changed from healthy to unhealthy.  
  
4.  In the **State Change Events Details** pane, you can see the error details that caused the health state change of your test.  
  
    > [!TIP]  
    > It is a good idea to check Health Explorer frequently because it shows you details about the context and sequence of status changes and errors.  
  
