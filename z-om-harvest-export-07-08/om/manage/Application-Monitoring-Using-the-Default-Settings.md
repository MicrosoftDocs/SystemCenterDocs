---
title: Application Monitoring Using the Default Settings
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abd195c1-584a-4eac-9c45-54ede7d36845
author:markgalioto
---
# Application Monitoring Using the Default Settings
Accepting all defaults can be a good way to start monitoring an application for which the administrator has very little or no knowledge. Then, after monitoring with all defaults for some time, the administrator can begin adjusting settings based on the monitoring alerts, Application Diagnostics data, and Application Advisor reports.  
  
## Using Default Settings for Server\-Side Monitoring  
You still need to select the application you want to monitor and the target management pack, but then you can start monitoring with “all defaults”. With all default settings Application Performance Monitoring will monitor only server\-side, and all thresholds for all pages will be the same. To see the default values, you can go through the wizard without changing anything.  
  
## Using Default Settings for Client\-Side Monitoring  
The defaults are enough to get this started and to allow you to test it out from localhost connections. It is simply scoped to monitor localhost by default.  
  
You can certainly accept the default settings for client\-side monitoring, but it is very important to run the compatibility check task to validate if the application can be monitored and if any of the pages should be excluded from monitoring. Therefore, simply applying of client\-side monitoring defaults might be risky. For more information about running the compatibility check task, see [Before You Begin Monitoring .NET Applications](../../om/manage/Before-You-Begin-Monitoring-.NET-Applications.md)  
  
In general, client\-side threshold settings should be higher than server\-side threshold settings. This is because the client\-side monitoring contains the server time, too. For instance, when a client\-side event is divided into various parts, some of the time is spent on the server, but the client also monitors the time spent on the network and the time spent in the browser.  
  
**IP Address Filters and Load balancers** Also, IP filters by default will enable client\-side monitoring for localhost only. Additionally, load balancer settings need to be set correctly for client\-side monitoring. If the IP header is not set, all client\-side monitoring traffic will appear to be coming from a single IP address. All IP\- and subnet\- based reports in Application Advisor will be invalid if the default settings are used with a load balancer.  
  
There is no default for the load balancers. The load balancer setting is one you can opt to change, whereas you must change the client IP filters because if you do not update those settings you will not get any data at all.  
  
**IP Address Filters** You can use client IP filters to choose the networks that you want to monitor. By applying filters, administrators can limit the scope of the monitored computers. By default, only localhost IP addresses are monitored. If the IP filter list is empty, all IP addresses are monitored. Any IP addresses that fit the filter definitions are excluded from client\-side monitoring. For more information, see [How to Configure IP Address Exclusion Filters for Client-Side Monitoring](../../om/manage/How-to-Configure-IP-Address-Exclusion-Filters-for-Client-Side-Monitoring.md)  
  
## See Also  
[Authoring Strategies for .NET Application Monitoring](../../om/manage/Authoring-Strategies-for-.NET-Application-Monitoring.md)  
[How to Start Monitoring a New Application](../../om/manage/How-to-Start-Monitoring-a-New-Application.md)  
  
