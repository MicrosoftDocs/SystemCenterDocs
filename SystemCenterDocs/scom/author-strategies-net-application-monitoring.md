---
ms.assetid: 77b54fbe-b6c3-4934-8b42-c89c08e3ccfd
title: Author Strategies for .NET Application Monitoring
description: This article provides an overview about authoring strategies for .NET application monitoring.
author: jyothisuri
ms.author: jsuri
ms.date: 07/24/2025
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Author strategies for .NET application monitoring

Here are some scenarios and settings to change during authoring that can help you receive the monitoring experience and data that is most helpful for you.

## Monitor a new application

Accepting all defaults can be a good way to start monitoring an application for which the administrator has little or no knowledge. Then, after monitoring with all defaults for some time, the administrator can begin adjusting settings based on the monitoring alerts, Application Diagnostics data, and Application Advisor reports. For more information, see [Start Monitoring a New Application](/previous-versions/system-center/system-center-2012-R2/hh544005%28v%3dsc.12%29) and [Application Monitoring Using the Default Settings](application-monitor-use-default-settings.md).

## Limit monitoring to a specific set of servers

Defining a targeted group allows you to limit monitoring to a specific set of servers. In the .NET Application Performance Monitoring wizard, targeted group for server-side monitoring is on the  **What to Monitor**  page. Targeted group for client-side monitoring is on the  **Enable Client-Side Monitoring**  page. If you're using a targeted group for client-side monitoring and use a load balancer, see [Client-Side Monitoring with Targeted Groups and Load Balancers](/previous-versions/system-center/system-center-2012-R2/hh544003%28v%3dsc.12%29).

For large application deployments, you typically don't need to monitor all instances of the application. A representative sample is enough to get the data you need. Using only a representative sample will keep the amount of data collected and stored lower.

## Reduce the "Noise"

Increasing the sensitivity threshold allows you to filter out fast-running methods, which reduce overall "noise", or how deep the call stack is going to go, making it easier for you to determine where the problem is. It also reduces network bandwidth usage.

The sensitivity setting is used to determine if a function call should be included in the call stack. Any function that executes and returns faster than the sensitivity level is dropped, keeping small fast-running functions from hiding the actual problem. Remember that using sensitivity only reduces the number of functions shown in the call stack for specific events, but an event will still be generated if the overall threshold is surpassed.

You can adjust the sensitivity threshold for server-side and client-side monitoring independently.

### Change the sensitivity threshold for server-side monitoring

To change the sensitivity threshold for server-side monitoring, follow these steps:

1. To open properties for the application group that you want to reconfigure, in the Operations Manager console, in the navigation pane, select the  **Authoring**  button, expand  **Management Pack Templates**, select  **.NET Application Performance Monitoring**, right-click the application group that you want to configure, and then select  **Properties**.

   > [!NOTE]
   > If you are currently authoring a new .NET Application Performance Monitoring template, to change the sensitivity threshold for server-side monitoring, go to the  **Server-Side Configuration**  page and select  **Advanced Settings**.  Change the  **Sensitivity threshold** and select  **OK**.

2. To change the sensitivity threshold for server-side monitoring, on the  **Properties**  page, select the  **Server-Side Monitoring**  tab, and then select the  **Advanced Settings**  button.
3. Change the  **Sensitivity threshold**  and select  **OK**.

### Change the sensitivity threshold for client-side monitoring

To change the sensitivity threshold for client-side monitoring, follow these steps:

1. To open properties for the application group that you want to reconfigure, in the Operations Manager console, in the navigation pane, select the  **Authoring**  button, expand  **Management Pack Templates** , select  **.NET Application Performance Monitoring** , right-click the application group that you want to want to configure, and then select  **Properties**.

    > [!NOTE]
    > If you're currently authoring a new .NET Application Performance Monitoring template, to change the sensitivity threshold for client-side monitoring, go to the  **Client-Side Configuration**  page and select  **Advanced Settings**. Change the  **Sensitivity threshold**  and select  **OK**.

2. To change the sensitivity threshold for client-side monitoring, on the  **Properties**  page, select the  **Client-Side Monitoring**  tab, and select the  **Advanced Settings**  button.
3. Change the  **Sensitivity threshold**  and select  **OK**.

It's also possible for high sensitivity to hide problems. In the situation where you've a function that calls another function, if the callee's response time increases even slightly, it might cause issues for the application. For example, if you've a data processing function that calls a lookup function 1,000 times and the lookup's processing time increases by 1 ms, you'll increase the response time for your top-level function by a full second. This might be masked by the high sensitivity. When you find this kind of situation, you can add the callee as a method and set a custom sensitivity for it to ensure it's always measured according to the lower sensitivity threshold.

Application failure alerts are application, or code, failures that are detected within the application. You can choose not to receive application failure alerts, which will potentially occur often if an application has problems because these kinds of alerts usually require code modifications to address. Turning this off reduces the "noise" of many alerts raised that can't be directly resolved by the operations team.

You can turn off application failure alerts for server-side and client-side monitoring independently.

### Turn off alerts for application failures for server-side monitoring

To turn off alerts for application failures for server-side monitoring, follow these steps:

1. To open properties for the application group that you want to reconfigure, in the Operations Manager console, in the navigation pane, select the  **Authoring**  button, expand  **Management Pack Templates** , select  **.NET Application Performance Monitoring** , right-click the application group that you want to want to configure, and then select  **Properties**.

   > [!NOTE]
   > If you're currently authoring a new .NET Application Performance Monitoring template, to turn off alerts for application failures for server-side monitoring, go to the  **Server-Side Configuration**  page and select  **Advanced Settings**. Clear the  **Application failure alerts**  checkbox and select  **OK**.

2. To turn off application failure alerts for server-side monitoring, on the  **Properties**  page, select the  **Server-Side Defaults**  tab, and select the  **Advanced Settings**  button.
3. On the  **Advanced settings**  page and clear the  **Application failure alerts**  checkbox.
4. Select  **OK**.

### Turn off alerts for application failures for client-side monitoring

To turn off alerts for application failures for client-side monitoring, follow these steps:

1. To open properties for the application group that you want to reconfigure, in the Operations Manager console, in the navigation pane, select the  **Authoring**  button, expand  **Management Pack Templates** , select  **.NET Application Performance Monitoring** , right-click the application group that you want to want to configure, and then select  **Properties**.

   > [!NOTE]
   > If you are currently authoring a new .NET Application Performance Monitoring template, to turn off alerts for application failures for client-side monitoring, go to the  **Client-Side Configuration**  page and select  **Customize**. On the  **Modifying Settings**  page, in the  **Transactions** section, select  **Add**. On the  **Transaction Properties**  page, clear the  **Application failure**  checkbox and select  **OK**.

2. To turn off application failure alerts for client-side monitoring, on the  **Properties**  page, select the  **Client-Side Monitoring**  tab, and select the  **Advanced Settings**  button.
3. In the  **Transactions**  section, select **Add**.
4. On the  **Transaction Properties**  page, clear the  **Application failure**
5. Select  **OK**.

## Only receive critical exceptions

By default, .NET Application Performance Monitoring defines critical exceptions as exceptions handled by specific exception handlers provided by the .NET framework. These handlers catch top-level ASP.NET exceptions and web service exceptions that the monitored application failed to catch and handle internally. By adding exception handlers, you're adding to what application monitoring's definition of what a critical exception is. In effect, any exceptions handled by these functions will be considered critical exceptions. The advantage to using exception handlers is that you maintain the benefit of streamlined reporting of critical exceptions only, but you have the additional benefit of reporting functions that are of interest to you. For more information and a list of default exception handlers, see [Use Exception Handlers to Define Critical Exceptions](use-exception-handlers-define-critical-exceptions.md).

## Improve client-side monitoring performance

You might also want to adjust the sampling rate to control the performance impact of the monitoring on your application with client-side monitoring. Reducing the sampling rate reduces the application monitoring traffic and helps conserve server resources. If you've even a low-traffic site, instrumenting and collecting data from every user who connects will result in a large amount of non-actionable data to sift through. Taking a random sample will give you the insight you need into the application performance from the client perspective without flooding you with a large amount of data to process and store.

### Change the sampling rate for client-side monitoring

To change the sampling rate for client-side monitoring, follow these steps:

1. To open client-side properties for the application group that you want to reconfigure, in the Operations Manager console, in the navigation pane, select the  **Authoring**  button, expand  **Management Pack Templates** , select  **.NET Application Performance Monitoring** , right-click the application group that you want to want to reconfigure, and then select  **Properties**.

   On the  **Properties**  page, select the  **Client-Side Defaults**  tab, and select the  **Advanced Settings**  button.

   > [!NOTE]
   > Because you can change the sampling rate for both the application group and each application component, changes to the application group settings will not automatically be applied to the component settings when the component settings have been previously customized.

2. In the  **Sampling**  section, use the dropdown menu to select the percentage of incoming requests that you want to monitor. For example, if you select  **50%**, you'll monitor 50 percent of the incoming requests. Select  **25%**  and you'll monitor 25 percent of the incoming requests, and so on. To get helpful information, you don't have to monitor all of the incoming requests.
3. When you have set the sampling rate, select  **OK**.

## Related content

[Start Monitoring a New Application](/previous-versions/system-center/system-center-2012-R2/hh544005%28v%3dsc.12%29).
