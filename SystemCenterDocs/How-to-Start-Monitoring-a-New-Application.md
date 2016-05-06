---
title: How to Start Monitoring a New Application
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc1f2e64-0fa0-4d7f-8127-1e4586b9e2d9
---
# How to Start Monitoring a New Application
When you have a new application that you are learning about, you can use the .NET Application Performance Monitoring template in [!INCLUDE[om12long](../Token/om12long_md.md)] to configure monitoring for it. Here are some settings to start with that will help you get to know your new application. In addition, it is ideal that you begin monitoring in a test or development environment.

## Monitoring Settings for a New Application
Following this strategy for monitoring a new application will help you get to know how the application behaves within your system and for your customer.

### Start Monitoring Server\-Side Only with a Simple Monitored System and Short\-Term Settings
First, keep the configuration simple: monitor one application on one server. Second, when you first configure .NET Application Performance Monitoring to monitor a new application, plan to keep the settings you implement long enough for you to understand some trends. A day’s worth of data should provide you with insight into the performance and usage patterns of the application.

### Establish Baseline Performance Using Default Settings and Some Specific Settings
For the most part, you will want to keep default settings. The default settings ensure that you will see any large issues with the application and keep the impact on the monitored application at a minimum.

If you are not getting any performance or exception events raised, you can use the following steps to get a feel for what the baseline performance looks like.

To begin monitoring, here are some settings you might want to adjust as noted here:

-   Lower the thresholds for performance. This will help you establish a baseline performance measure by seeing what the current performance characteristics of the application are.

-   Enable all namespaces. You want to find out what namespaces are involved and if you set specific namespaces at first, you might miss a namespace where an error is occurring.

-   Collect all exceptions, not just critical exceptions. You need to know what kinds of exceptions are being thrown. Using known exception handlers limits the exceptions you will receive.

This can result in a lot of data—more than you would want for long\-term monitoring—but at first, this amount of data will be helpful as you will see trends, such as the kinds of paths customers are taking through the system and what normal performance looks like.

With the data collection complete, use the Application Advisor reports, such as Application Performance Analysis, to see how the monitored applications are looking. Using the report you will see what the average duration is for the heaviest \(longest running\) calls through the system as well as the maximum amount of time spent processing requests. This allows you to set customized smart thresholds based on real application performance. You will also see which functions are running faster than others, and you can create specific web page, web method, and function transactions for the critical methods so that you can ensure they are responding under a tighter SLA than the application as a whole. For more information on viewing reports, see how to scope and run and Application Advisor report in Prioritizing Alerts by Using Application Advisor.

### Adjust Settings and Compare to the Baseline
Once you have established a baseline performance measure, begin to adjust the settings to tune the monitoring so it catches the kinds of exceptions that are being raised. By reporting all exceptions, you will see if there are any default exception handlers in the application that are catching exceptions for which you would prefer receiving alerts. The data you get will be more meaningful and lower in volume with each adjustment.

-   Remove the custom settings and set thresholds based on the data collected.

-   Add specific namespaces based on the call stacks in the performance and exception events you found during the baseline phase.

-   Add exception handlers for any application level “catch all” handlers that keep exceptions from going outside the application and to the .NET Framework exception handlers.

-   Add specialized transactions to monitor the performance of common methods that should be held to a stronger SLA than the application as a whole.

Compare the new data to your baseline. You will begin to see the real average response time, for instance. Now that you know the various performance exceptions the application is sending, you can add the specific namespaces you want rather than monitoring all namespaces. Your application will be configured to be monitored based on the observed performance levels and will be alerted if things move outside of normal levels.

### Gradually Deploy the Application to More Monitored Servers in Your System
After monitoring the application for a time with the new monitoring configuration, when you feel your application is healthy, increase the number of servers you are running the application on and monitoring from one to 10, for example. Once you have it running healthy at that level, increase the deployment and monitoring to more servers, and so on. This gradual rollout approach will help you gain confidence in the monitoring for that application and help ensure the health of your system.

### Begin Client\-Side Monitoring
When you are confident that your application is running well within your system, it’s a good time to monitor what the customer experiences. This is what client\-side application monitoring does. To enable client\-side monitoring, see [How to Configure Monitoring for .NET Applications](../Topic/How-to-Configure-Monitoring-for-.NET-Applications.md)

### What the Operator can do with This Information
Using this basic information, the operator can have a better idea where the problem is with the application or with the infrastructure and know whether it is something only to the development team can fix or the operator can address directly.

## See Also
[How to Add, Enable, and Disable Namespaces](../Topic/How-to-Add,-Enable,-and-Disable-Namespaces.md)
[Using Exception Handlers to Define Critical Exceptions](../Topic/Using-Exception-Handlers-to-Define-Critical-Exceptions.md)
[Authoring Strategies for .NET Application Monitoring](../Topic/Authoring-Strategies-for-.NET-Application-Monitoring.md)
[Application Monitoring Using the Default Settings](../Topic/Application-Monitoring-Using-the-Default-Settings.md)

