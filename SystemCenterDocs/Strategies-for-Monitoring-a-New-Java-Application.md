---
title: Strategies for Monitoring a New Java Application
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 262cd9b5-f651-4ba5-a5a7-a6a05baf9eef
---
# Strategies for Monitoring a New Java Application
Here are some scenarios and settings to change during authoring that can help you receive the monitoring experience and data that are most helpful for you.

## Monitoring a New Application for which the Administrator has Little Knowledge
Accepting all defaults can be a good way to start monitoring an application for which the administrator has very little or no knowledge. Then, after monitoring with all defaults for some time, the administrator can begin adjusting settings based on the monitoring alerts, Application Diagnostics data, and Application Advisor reports. For more information, see [How to Monitor Java Applications](./How-to-Monitor-Java-Applications.md).

## Limit Monitoring to a Specific Set of Servers
Defining a targeted group allows you to limit monitoring to a specific set of servers. For very large application deployments, you typically do not need to monitor all instances of the application. A representative sample is enough to get the data you need. Using only a representative sample will keep the amount of data collected and stored lower.

## Reduce the “Noise” by Defining How Much Data You Collect
Increasing the sensitivity threshold allows you to filter out fast\-running methods, which reduces overall “noise”, or how deep the call stack is going to go, making it easier for you to determine where the problem is. It also reduces network bandwidth usage.

The sensitivity setting is used to determine if a function call should be included in the call stack. Any function that executes and returns faster than the sensitivity level is dropped, keeping small fast\-running functions from hiding the actual problem. Remember that using sensitivity only reduces the number of functions shown in the call stack for specific events, but an event will still be generated if the overall threshold is surpassed.

You can adjust the sensitivity threshold in the configuration file as discussed in the Management Pack Guide for Java Application Performance Monitoring.

It is also possible for high sensitivity to hide problems. In the situation where you have a function that calls another function, if the callee’s response time increases even slightly, it might cause issues for the application. For example, if you have a data processing function that calls a lookup function 1,000 times and the lookup’s processing time increases by 1 ms, you will increase the response time for your top level function by a full second. This might be masked by the high sensitivity. When you find this kind of situation, you can add the callee as a method and set a custom sensitivity for it to ensure it is always measured according to the lower sensitivity threshold.

Application failure alerts are application, or code, failures that are detected within the application. You can choose not to receive application failure alerts, which will potentially occur very often if an application has problems because these kinds of alerts usually require code modifications to address. Turning this off reduces the “noise” of many alerts raised that cannot be directly resolved by the operations team.

## See Also
[How to Monitor Java Applications](./How-to-Monitor-Java-Applications.md)
[How to Configure Monitoring for Java Applications](./How-to-Configure-Monitoring-for-Java-Applications.md)
[Monitoring .NET Applications](./Monitoring-.NET-Applications.md)


