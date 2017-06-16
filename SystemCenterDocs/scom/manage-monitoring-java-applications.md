---
title: Monitoring Java Applications
description: This article describes the concepts and recommendations for monitoring Java applications with Operations Manager.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 06/16/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
ms.assetid: 13f2661d-ad31-4d01-92b4-fb9b2e7173f8
---
# Monitoring Java applications
Java Application Performance Monitoring (APM) in System Center 2016 - Operations Manager lets you monitor Java applications to get details about application performance and exception events that can help you determine the root causes of problems. The System Center 2012 and 2016 Management Pack for Java Application Performance Monitoring lets you monitor Java application performance and exception events by using Operations Manager Application Advisor. With Operations Manager Application Advisor, you can investigate method and resource timing for performance events, stack traces for exception events, Java-specific counters for events (such as Average Request Time, Requests Per Second, JVM Memory, and Class Loader), and run some of the standard Application Performance Monitoring reports. Additionally, you get Operations Manager level alerting on Java application server counters. Download the Management Pack for Java Application Performance Monitoring from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=313918).  
  
Java Application Performance Monitoring shares many concepts with .NET Application Performance Monitoring. However, there are some important differences, including: object hierarchy, the method for working with overrides and alerting (Java Application Performance Monitoring has no authoring and configuration template, so you change configurations with management pack overrides), and sever-level information is not handled in Java Application Performance Monitoring reports.  
  
## Supported configurations  
The Management Pack for Java Application Performance Monitoring requires Windows Server 2012 R2 and Operations Manager.  
  
Supported configurations:  
  
-   Tomcat 5, Tomcat 6, and Tomcat 7  
  
    -   Windows  
  
    -   Linux  
  
-   Java JDK 5, Java JDK 6  
  
-   Web Technologies  
  
    -   GenericServlet  
  
    -   Struts  
  
    -   Struts2  
  
    -   Axis2  
  
## Prerequisites  
To run the Management Pack for Java Application Performance Monitoring, you must have the Management Pack for Java Enterprise Edition (JEE) configured for deep monitoring. This management pack monitors JEE application servers and provides initial application level discovery. For more information, see [How to Configure Monitoring for Java Applications](manage-configure-monitoring-java-applications.md) and the Management Pack Guide for JEE for your particular type of application server, available on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=325020).  
  
## How to monitor Java applications
When you have a new Java application that you are learning about, you use Java Application Performance Monitoring to get baseline measures before you gradually scale up deployment. Here are some settings to start with that helps you get to know your new application. In addition, it is ideal that you begin monitoring in a test or development environment to establish a baseline configuration before implementing in production.    
  
## Monitoring settings for a new application  
Following this strategy for monitoring a new Java application will help you get to know how the application behaves within your system and for your customer.  
  
### Start monitoring with a simple monitored system and short-term settings  
First, keep the configuration simple: monitor one application on one server. Second, when you first configure Java Application Performance Monitoring to monitor a new application, plan to keep the settings you implement long enough for you to understand some trends. A day's worth of data should provide you with insight into the performance and usage patterns of the application.  
  
### Establish baseline performance using default settings and some specific settings  
Usually, you will want to keep default settings. The default settings ensure that you will see any large issues with the application and keep the impact on the monitored application at a minimum.  
  
If you are not getting any performance or exception events raised, you can use the following steps to get a feel for what the baseline performance looks like.  
  
To begin monitoring, here are some settings you might want to adjust as noted here:  
  
-   Lower the thresholds for performance. This helps you establish a baseline performance measure by seeing what the current performance characteristics of the application are. For more information about performance thresholds, see [How to Configure Monitoring for Java Applications](manage-configure-monitoring-java-applications.md).  
  
-   Examine all exceptions. You need to know what kinds of exceptions are being thrown. Using known exception handlers limits the exceptions you will receive.  
  
This can result in signifcant data, more than you would want for long-term monitoring.  Initially, this amount of data will be helpful as you will see trends, such as the kinds of paths customers are taking through the system and what normal performance looks like.  
  
With the data collection complete, use the Application Advisor reports, such as Application Performance Analysis, to see how the monitored applications are looking. Using the report you will see what the average duration is for the heaviest (longest running) calls through the system as well as the maximum amount of time spent processing requests. This allows you to set customized smart thresholds based on real application performance. You will also see which functions are running faster than others, and you can create specific web page, web method, and function transactions for the critical methods so that you can ensure they are responding under a tighter SLA than the application as a whole. For more information on viewing reports, see how to scope and run an Application Advisor report in [Prioritizing Alerts by Using Application Advisor](manage-prioritizing-alerts-using-application-advisor.md).  
  
### Adjust settings and compare to the baseline  
Once you have established a baseline performance measure, begin to adjust the settings to tune the monitoring so it catches the kinds of exceptions that are being raised. By reporting all exceptions, you will see if there are any default exception handlers in the application that are catching exceptions for which you would prefer receiving alerts. The data you get will be more meaningful and lower in volume with each adjustment.  
  
-   Remove the custom settings and set thresholds based on the data collected.  
  
-   Add exception handlers for any application level "catch all" handlers that keep exceptions from going outside the application.  
  
-   Add specialized transactions to monitor the performance of common methods that should be held to a stronger SLA than the application as a whole.  
  
Compare the new data to your baseline. You will begin to see the real average response time, for instance. Now that you know the various performance exceptions the application is sending, you can add the specific namespaces you want rather than monitoring all namespaces. Your application will be configured to be monitored based on the observed performance levels and will be alerted if things move outside of normal levels.  
  
### Gradually deploy the application to more monitored servers  
After monitoring the application for a time with the new monitoring configuration, when you feel your application is healthy, increase the number of servers you are running the application on and monitoring from one to 10, for example. Once you have it running healthy at that level, increase the deployment and monitoring to more servers, and so on. This gradual rollout approach will help you gain confidence in the monitoring for that application and help ensure the health of your system.  
  
### What the operator can do with this information  
Using this basic information, the operator can have a better idea where the problem is with the application or with the infrastructure and know whether it is something only to the development team can fix or the operator can address directly.  
  

## Next steps
For details about configuring monitoring of Java applications, see [How to Configure Monitoring for Java Applications](manage-configure-monitoring-java-applications.md).  