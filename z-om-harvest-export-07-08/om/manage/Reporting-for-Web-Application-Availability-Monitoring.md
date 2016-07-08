---
title: Reporting for Web Application Availability Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a15fc3c-c096-4ea1-b768-2df47289a44a
author:markgalioto
---
# Reporting for Web Application Availability Monitoring
Web Application Availability Monitoring introduces to two new report tasks: Test Availability and Test Performance. The Test availability reporting shows measures reflecting how available the web application was over time. The Test Performance report shows selected objects and performance counter values over time to relate how well a web application has performed. These two reports directly reflect the web application monitoring for Web Application Availability is integrated into the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, you can run these two new reports just as you would run the other standard [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] reports.  
  
### To run the Test Availability report  
  
1.  You can run the Test Availability report from several locations:  
  
    -   In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, click **Application Monitoring**, click **Web Application Availability Monitoring**, and then click **Active Alerts**, **Test State**, or **Web Application Status** to display alerts or status for the category. Highlight one or more web applications, alerts, or test states, and then, in the **Tasks** pane, in the **Report Tasks** section, click **Test Availability**.  
  
    -   If you want to add more objects, click **Add Object**, and in the **Add Object** page, filter your search or just click **Search** to see all tests in for the web application that you have selected. Click the available items you want to include in your report and click **Add**. Click **OK**.  
  
    -   In the **Summary Dashboard** view, click to highlight an item in the **Test Status**, and then run the report task from the **Tasks** pane.  
  
    -   In the **Details Dashboard**, click to highlight an item, and then run the report task from the **Tasks** pane.  
  
2.  In the **Aggregation** section of the **Test Availability** report configuration page, select how often you want information aggregated and a time and date range.  
  
    > [!NOTE]  
    > The data warehouse only aggregates data hourly for 100 days. After 100 days, data are aggregated daily.  
  
3.  Select the aspects, such as **Unplanned Maintenance**, that you would like to include in the report, and then click **Run** to generate the report.  
  
4.  In the report, click a plus sign to see details. To see a graph of the data, click the **Availability Tracker** link.  
  
### To run the Test Performance report  
  
1.  You can run the Test Performance report from several locations:  
  
    -   In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Monitoring** button, click **Application Monitoring**, click **Web Application Availability Monitoring**, and then click **Active Alerts**, **Test State**, or **Web Application Status** to display alerts or status for the category. Highlight one or more web applications, alerts, or test states, and then, in the **Tasks** pane, in the **Report Tasks** section, click **Test Performance**.  
  
    -   If you want to add more objects, click **Add Object**, and in the **Add Object** page, filter your search or just click **Search** to see all tests in for the web application that you have selected. Click the available items you want to include in your report and click **Add**. Click **OK**.  
  
    -   In the **Summary Dashboard** view, click to highlight an item in the **Test Status**, and then run the report task from the **Tasks** pane.  
  
    -   In the **Details Dashboard**, click to highlight an item, and then run the report task from the **Tasks** pane.  
  
2.  In the **Aggregation** section of the **Test Performance** report configuration page, select how often you want information aggregated and a time and date range.  
  
    > [!NOTE]  
    > The data warehouse only aggregates data hourly for 100 days. After 100 days, data are aggregated daily.  
  
3.  To generate the report, click **Run**.  
  
4.  In the report, click a plus sign to see details.  
  
