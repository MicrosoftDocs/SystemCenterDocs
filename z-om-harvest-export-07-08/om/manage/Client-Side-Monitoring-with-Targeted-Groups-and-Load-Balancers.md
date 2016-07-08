---
title: Client-Side Monitoring with Targeted Groups and Load Balancers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 474bdebf-6bbc-429f-a791-a382d95113bc
author:markgalioto
---
# Client-Side Monitoring with Targeted Groups and Load Balancers
When load balancers are used during client\-side monitoring, the load balancer is designed to get the true client IP addresses. In a simple case, when a client is connected directly to one web server, the web server knows the client IP address. However, when you have several servers and use a load balancer to distribute traffic from the clients among the servers, this can present two problems. First, the IP reported to the collector is the virtual IP that the load balancer uses, not the real end\-user IP. When users hit the load balancer, it sends them to an appropriate web server. Due to the load balancer, the web server sees only the internal port IP \(inside the network\), not the real IP \(outside the network\). Additionally, if some servers are monitored and some are not, data can be lost because responses from the clients are often sent to servers in a least load or round robin fashion, which means that the response might go to a server that is not hosting a collector.  
  
Here are some strategies for setting up client\-side monitoring when you have multiple monitored servers and use load balancers.  
  
## Monitoring with a Load Balancer and Targeted Group  
When you configure client\-side monitoring, you have the option to set the target group, limiting the number of web servers used for monitoring. In this scenario, only monitored servers in the target group will inject the JavaScript used for monitoring and the servers outside the target group that are not monitored will not get instrumented when using load balancers with the web servers. This results in having incorrect data. The load balancer does not know which servers are inside or outside the targeted group and sends client requests to servers that are both inside \(monitored\) or outside \(unmonitored\) of the targeted group. The result is that requests that have been instrumented and try to return data to the collectors might send their results to servers that cannot handle the data.  
  
-   **Solution 1** If you are authoring a new .NET Application Performance Monitoring template and including client\-side monitoring for a targeted group, we recommend that you choose a group of servers that are all served by the same load balancer. Target monitoring to all servers in the load\-balanced farm.  
  
-   **Solution 2** If you are already running client\-side monitoring with a targeted group and a load balancer, you can resolve this issue by creating a rule on the load balancer that directs all of the monitoring traffic to the monitored servers. Monitoring traffic is the monitoring JavaScripts that send data to the collector endpoint. You can identify monitoring traffic because it contains **\/CSMCollector** in the URL. Each load balancer has its own model for configuring rules. Refer to your load balancer’s documentation for details about how to create the rule.  
  
