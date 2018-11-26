---
title: "Global Service Monitor | Microsoft Docs"
ms.custom: ""
ms.date: 4/26/2018
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.tgt_pltfrm: ""
ms.topic: article
applies_to: System Center 2016 - Operations Manager
ms.assetid: 147a3ec0-43e7-4cd7-afcf-384a3476f9f4
author: jyothi
ms.author: magoedte
manager: carmonm
---

# Global Service Monitor
[!INCLUDE[gsmlong](../includes/gsmlong-md.md)] is a cloud service that provides a simplified way to monitor the availability of external-web-based applications from multiple locations around the world. Importantly, [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] monitors applications from the perspective of the customers who use them. Because [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] monitors from locations that are correlated to customer geographies, application owners can gain insight into customer experiences in addition to the separate problems related to external factors, such as Internet or network problems, from application or service problems. The [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] monitoring experience focuses on the application instead of the infrastructure or individual URL.  
  
 [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] integrates with the [!INCLUDE[om12short](../includes/om12short-md.md)] console so that you can monitor external- and internal-facing web applications in the same place you monitor other applications.  
  
## [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] Monitoring Capabilities  
 With [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], the [!INCLUDE[om12short](../includes/om12short-md.md)] console integration lets you monitor web applications from both internal and external locations. In [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], you can use your management group and obtain access to agents in the cloud provided by Microsoft. This lets you monitor web applications from 16 locations and then report back to your management group. You can also use your own agents as watcher nodes to monitor internal locations and applications.  
  
 **Two kinds of monitoring**  
  
 [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] is set to provide you a maximum number of tests for the two monitoring types. These are the Web Application Availability monitoring that monitors single URLs, and Visual Studio Web Tests monitoring that lets you to run multi-step, authenticated web tests from Microsoft-provided agents in the cloud. In the version of [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], Visual Studio Web Tests can be run from 16 external locations.  
  
> [!NOTE]
>  To view a web test result that you download from [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], you must be running Microsoft Visual Studio Ultimate 2012 or Visual Studio Ultimate 2010 with these additions:  
>   
> - If your test controller crashes or stops responding when you run web tests in Visual Studio 2010, [download and install this hotfix](http://go.microsoft.com/fwlink/?LinkId=271586).
> - Install this hotfix: [http://hotfixv4.microsoft.com/Visual Studio 2010/sp1/DevDiv954543/40219.363/free/441527_intl_i386_zip.exe](http://hotfixv4.microsoft.com/Visual Studio 2010/sp1/DevDiv954543/40219.363/free/441527_intl_i386_zip.exe)  
  
## Test Maximums and Locations  
 For Web Application Availability monitoring, a test is defined as one URL from one location. For Visual Web Tests monitoring, a test is defined as one .webtest file from one location. For both monitoring types, the total number of tests equals the number of tests that you monitored multiplied by the number of locations from which you monitor. You can run each test as frequently as you want at intervals of 5 minutes or more. One test every 5 minutes is the minimum supported test interval for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)]. Only the maximum supported number of tests will remain monitored. Additional tests will not be monitored and tests that exceed the maximums are displayed as “not monitored” in the [!INCLUDE[om12short](../includes/om12short-md.md)] console. Additionally, you will receive alerts related to exceeding the maximum supported number of tests. To view these alerts, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Monitoring**, expand **[!INCLUDE[om12short](../includes/om12short-md.md)]**, and then click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**.  
  
> [!NOTE]
>  Test maximums and locations are subject to change.  
  
To see how many tests you have scheduled, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Administration**, and then click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**.  
  
Test parameters for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] Web Application Availability monitoring tests include the following:  
  
-   Total tests are the number of tests multiplied by the number of locations.  
-   In a GSM subscription, the total number of tests cannot exceed 25. You can't have more than 10 tests in any location.
-   Minimum interval per tests must be greater than or equal to 5 minutes.
-   Global test timeout: 30 seconds.  
  
Test parameters for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] Visual Studio Web Tests monitoring tests include the following:  
  
-   Total tests are the number of .webtest files multiplied by the number of locations.
-   In a GSM subscription: the total number of tests cannot exceed 25. You can't have more than 3 tests in any POP location.
-   Minimum interval per tests must be greater than or equal to 5 minutes.
-   Maximum number of requests per web test: 100.
-   Maximum web test file size: 100 kilobytes (KB).

 Subscriptions per tenant:
-   GSM subscription: 5  
  
 With [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], you can test from 16 locations by selecting from the following:
        -   Australia East
        -   Brazil South
        -   Central US
        -   East Asia
        -   East US
        -   France Central
        -   France South
        -   Japan East
        -   North Central US
        -   North Europe
        -   South Central US
        -   Southeast Asia
        -   UK South
        -   UK West
        -   West Europe
        -   West US   
  
## Important Things to Know  
  
-   To use [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], you must have [!INCLUDE[om12long](../includes/om12long-md.md)] installed.  
  
-   For Web Application Availability Monitoring, only public-facing URLs (that do not require authentication) are supported in provided locations. Internal-facing URLs can be monitored by using internal agents as watcher nodes in the network.  
  
-   If you configure the specified above quota of tests, additional tests will not be run. The console displays tests that exceed the maximums as “not monitored” and you will get an alert notifying you that you exceeded the allowed number of tests.  
  
-   The web application name is part of the performance counter instance name. If you rename your web application, the performance counter instance names will also change. This causes data in the performance view to be split across the different counter names. Dashboards show only the latest values from the performance counter and the previous data is no longer displayed.  
  
-   We recommend that you use at least two locations for each test in case one location stops functioning temporarily.  
  
#### See Also
  
-   [Getting Started with Global Service Monitor: Signing In and Setup](../gsm/getting-started-with-global-service-monitor-signing-in-and-setup.md)
-   [Configuring Tests in Global Service Monitor](../gsm/configuring-tests-in-global-service-monitor.md)
-   [Monitoring Tests and Alerts for Global Service Monitor](../gsm/monitoring-tests-and-alerts-for-global-service-monitor.md)
-   [Dashboard Views in Global Service Monitor](../gsm/dashboard-views-in-global-service-monitor.md)
-   [Downloading and Sharing Global Service Monitor Web Tests and Results](../gsm/downloading-and-sharing-global-service-monitor-web-tests-and-results.md)
-   [System Center Global Service Monitor for System Center 2012 Operations Manager Privacy Statement](http://go.microsoft.com/fwlink/?LinkId=275124)
-   [Global Service Monitor Service Level Agreement (SLA)](http://go.microsoft.com/fwlink/?LinkId=275121)
-   [Online Services Supplemental Terms and Conditions](http://go.microsoft.com/fwlink/?LinkId=275484)
