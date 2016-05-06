---
title: How to Configure Monitoring for .NET Applications
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18139dea-ce84-42b8-bd50-d467d72623e1
---
# How to Configure Monitoring for .NET Applications

## Configure .NET Application Performance Monitoring
The **.NET Application Performance Monitoring** template in [!INCLUDE[om12long](../Token/om12long_md.md)] lets you monitor .NET and WCF applications hosted in Internet Information Services \(IIS\) 7.0. [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] You monitor applications hosted in IIS 8.0 and Windows Services. You can select one or more applications or services and configure monitoring of performance and exception events. Server\-side monitoring lets you measure details about the performance and reliability of applications that are running in your datacenter. By monitoring client\-side applications, you can measure details of the customer experience, such as how long it takes for a page to load. It is another way to monitor how your applications are working from the perspective of your customer. Client\-side application monitoring helps you determine whether your users are experiencing problems. With both client\-side and server\-side monitoring in use, you can determine if a problem exists on your server, in the application, or is being caused by external factors, such as high network latency.

> [!TIP]
> Client\-side monitoring can be set up at the same time as server\-side monitoring when you run the .NET Application Performance Monitoring wizard or by editing an existing instance of a template.

> [!IMPORTANT]
> You can only configure client\-side monitoring for applications that have been configured for server\-side monitoring.

#### To configure .NET Application Performance Monitoring \(server\-side perspective\)

1.  To open the **.NET Application Performance Monitoring** template, in the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, click **.NET Application Performance Monitoring**, and then, in the tasks pane, click the **Add Monitoring Wizard** where you name and configure the application group that you want to monitor.

    **Location of .NET Application Performance Monitoring**

    ![](../Image/AppMonitoring_APMTempLocation.gif)

2.  In the **Add Monitoring Wizard** on the **Monitoring Type** page, select **.NET Application Performance Monitoring**, and then click **Next**. This template lets you monitor web applications and services hosted in IIS 7.0. \([!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] You can monitor applications hosted in IIS 8.0 and Windows Services.\) You can select one or more applications or services discovered by the IIS 7.0 management pack and configure monitoring of performance and exception events. [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] You can select one or more applications or services discovered by the IIS 8.0 management pack or Windows Services previously configured with the Windows Service Template.

3.  On the **General Properties** page, enter a friendly name and description for the application group that you are creating.

    In the **Select destination management pack** menu, select the management pack to store the settings that are specific to this instance of the template. To create a new management pack, click **New**. In the **Create a Management Pack** wizard, name your new management pack the same as the application group so you can easily pair the two, which is helpful later in the monitoring experience. Click **Next**. For more information, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

4.  On the **What to Monitor** page, in the **Application components** section, click **Add**. On the **Object Search** page, on the **Search for** menu, use the **Filter by part of the name \(optional\)** box to narrow your search, and then click **Search** to view a list of the application components you can monitor. \([!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] You can monitor Windows Services.\) From the search results, select the application components that you want to monitor, click **Add**, and then click **OK**. The application components you selected are now displayed as members of the application group that you are going to monitor. Click **Next**.

    On the **What to Monitor** page, on the **Environment** menu, select the environment you want to monitor your application in: **None**, **Production**, **Staging**, **Test**, **Development**, or **New**. Typically, you want to pair the environment tag with the server group you are monitoring.

    > [!TIP]
    > If you do not have to monitor multiple versions of the same applications, such as production instances and staging instances, you can leave the environment tag set to **None**.

5.  To limit the scope of monitoring to a group of servers, on the **What to Monitor** page, in the **Monitored Servers** section, click **Search**. On the **Group Search** page that opens, select the **Filter by** box and **Management pack** menu to find the server group that you want to use, and then click **Search**. Select the server group to which you want to limit monitoring in the **Available Groups** search results list, and click **OK** to add it to your targeted server group to monitor. Click **Next**.

    > [!TIP]
    > The **Targeted servers** group lets you configure monitoring by using one set of thresholds for one set of application servers and a different set of thresholds for another set of application servers. To configure monitoring for the second set of application servers, run the template again, and use the alternate **Targeted servers** group and use a different environment tag for each template instance.

6.  On the **Server\-Side Configuration** page, decide how you want to configure your monitoring. You have options to:

    -   Turn on or off performance event monitoring

    -   Turn on or off exception event monitoring

    -   Change the Performance Event Threshold

    -   Configure Advanced Settings

    -   Enable additional configuration options for server\-side and client\-side monitoring.

7.  To further configure exception and performance event monitoring for the application group, including settings for **Namespaces**, **Methods**, **ExceptionTracking**, and **Critical Exception Handlers**, click **Advanced Settings**. Also on the **Advanced Settings** for **Server\-Side Monitoring** page, you can reset monitor thresholds from the defaults and scope monitoring to a targeted group. If you want to use or return to the default **Advanced Settings**, click **Use Default Configuration**. When you are finished, click **OK**. For more information, see [How to Start Monitoring a New Application](../Topic/How-to-Start-Monitoring-a-New-Application.md) and [Application Monitoring Using the Default Settings](../Topic/Application-Monitoring-Using-the-Default-Settings.md)

    > [!WARNING]
    > Gathering detailed performance and exception events can lead to collecting sensitive information that should not be passed on to the development team. For example, if you capture an exception from your billing system, you might also capture user names and other tokens that can be used to identify the person who is having problems making purchases and what they were trying to purchase. Before enabling the collection of parameters and local variables for performance and exception events, we recommend that you review your policies. For more information, see [Working with Sensitive Data for .NET Applications](http://go.microsoft.com/fwlink/?LinkId=231757)

8.  If you only want to configure server\-side monitoring and do not want to customize additional server\-side monitoring options or configure and enable client\-side monitoring, click **Next**, and on the **Summary** page, review your monitoring configuration for your application group. To create the monitoring template, click **Create**.

9. You might have to restart IIS or recycle the application pools to finalize the configuration of the applications for monitoring. If a restart or recycle is required, you receive an alert and can use the task link in the knowledge base to perform the necessary action.

    > [!NOTE]
    > After you restart the application it does not begin collecting information accessed by users.

10. If you do want to customize server\-side monitoring settings further and to configure and enable client\-side monitoring, select the **Enable additional configuration options for server\-side and client\-side monitoring** check box, and then click **Next**. This command adds pages to the wizard as described below.

## Additional Customization for .NET Application Performance Monitoring \(Server\-Side Perspective\)
Using the **Modifying Settings** page, you can customize server\-side monitoring settings for specific application components.

#### To customize .NET Application Performance Monitoring for a specific application component \(server\-side perspective\)

1.  If you want to customize server\-side monitoring settings further and to configure and enable client\-side monitoring, on the **Server\-Side Configuration** page, select the **Enable additional configuration options for server\-side and client\-side monitoring** check box, and then click **Next**. This command adds pages to the wizard.

    > [!WARNING]
    > If you do not want to change settings of an application component monitor, click **Next**, and continue with **Client\-Side Configuration**.

2.  To select the specific application component for which you want to customize monitoring, on the **Server\-Side Customization** page, click **Customize**. The **Modifying Settings** page lets you customize and specialize monitoring for the specific application component and create transactions for individual webpages, web methods, or functions within the application component. When you are finished, click **OK**, and then click **Next**. If you do not want to configure and enable client\-side monitoring, click **Next** on the **Client\-Side Configuration** page, and then click **Next** on the **Enable Client\-Side Monitoring** page.

3.  On the **Summary** page, review your monitoring configuration for your application group. To create the monitoring template, click **Create**.

4.  You might have to restart IIS or recycle the application pools to finalize the configuration of the applications for monitoring. \([!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] You might have to restart the Windows Service.\) If a restart or recycle is required, you receive an alert and can use the task link in the knowledge base to perform the necessary action.

    > [!NOTE]
    > After you restart the application it does not begin to collect information until it is accessed by users.

## Enable and Configure .NET Application Performance Monitoring \(Client\-Side Perspective\)
Client\-side application monitoring lets you measure details of the customer experience, such as how long it takes for a page to load. It is another way to monitor how your applications are working from the perspective of your customer. Client\-side application monitoring helps you determine whether a problem exists on your server, in the application, or elsewhere.

> [!IMPORTANT]
> You can only configure client\-side monitoring for applications that have been configured for server\-side monitoring.

> [!IMPORTANT]
> When working with web applications configured using IIS Shared Configuration, the [!INCLUDE[om12short](../Token/om12short_md.md)] “Privileged Monitoring Account” Runas Profile associated with the Windows agents hosting the application must have read and write permissions on the shared directory that hosts the web application files to create the Client\-Side Monitoring Collector web application, as well as local administrative privileges on each server in the farm to access the IIS metabase for discovery.

> [!TIP]
> Client\-side monitoring can be set up at the same time as server\-side monitoring when you run the .NET Application Performance Monitoring wizard or through editing an existing instance of a template as described below.

#### To enable and configure .NET Application Performance Monitoring \(client\-side perspective\)

1.  You can either enable client\-side monitoring as part of the .NET Application Performance Monitoring Wizard when you configure monitoring for server\-side monitoring, or you can revise an existing template to include client\-side monitoring. This procedure describes how to enable client\-side monitoring while authoring the template.

    To enable client\-side monitoring, on the **Server\-Side Configuration** page, select the **Enable additional configuration options for server\-side and client\-side monitoring** check box and continue with the wizard.

    To revise the template to add client\-side monitoring, see [To add client\-side monitoring to an existing .NET Application Performance Monitoring template](../Topic/How-to-Configure-Monitoring-for-.NET-Applications.md#BKMK_AddCSM)

2.  On the **Client\-Side Configuration** page, you can select to turn on performance and exception event alerts, set page load thresholds and the Ajax and WCF threshold for the application group you are going to monitor. What you enter in the **Configure client IP address filter** section determines the client requests that are monitored. You can use client IP filters to select the networks that you want to exclude from monitoring. By applying filters, administrators can limit the scope of the monitored computers. By default, the filter is set to localhost, so only connections from browsers started on the local server are instrumented for monitoring. If the IP filter list is empty, all IP addresses are monitored. Any IP addresses that fit the filter definitions are excluded from client\-side monitoring. For more information and filtering examples, see [How to Configure IP Address Exclusion Filters for Client-Side Monitoring](../Topic/How-to-Configure-IP-Address-Exclusion-Filters-for-Client-Side-Monitoring.md).

3.  To configure more settings for this application group, click **Advanced Settings**. Here, in addition to settings on the previous page, you can set the sensitivity threshold, that lets you filter out fast\-running methods, which reduces overall “noise”, making it easier for you to determine where the problem is and reduces network bandwidth usage. You can also choose to sample only a percentage of the incoming requests. Choosing to monitor only some of the incoming requests can help reduce the load on your monitoring server. Additionally, you can configure these settings:

    -   In the **Monitors** section, you can change the default thresholds and intervals for the monitors.

    -   In the **Data collection** section, you can select the type of data you want to collect.

        > [!WARNING]
        > Enabling the **Exception Stack** and **Global Variables** data collection sends application data to the monitored server. We recommend that you do not enable the data collection from **Exception Stack** and **Global Variables** unless the application is configured to use an HTTPS protocol.

    -   **Load balancer settings** let you select the type of load balancers that you are using with your application. You can also add your own load balancer, if it is not included in the list. For more information about load balancers, see [Client-Side Monitoring with Targeted Groups and Load Balancers](../Topic/Client-Side-Monitoring-with-Targeted-Groups-and-Load-Balancers.md)

    -   In the **Monitored Servers** section, you can target a group to limit the scope of the monitoring to a group of servers. To select a targeted group, click **Search** and use the **Group Search** page to search for the group by name and management pack, and then add them to the selected objects list. The targeted group you select consists of only the servers hosting the web application that set the application pages to return browser\-side events. This group lets you limit client\-side monitoring independent of server\-side monitoring.

    > [!TIP]
    > Only applications hosted on servers that are members of both the server\-side and client\-side targeted groups are monitored by client\-side monitoring.

    When you have made your changes, click **OK**, and then click **Next**.

4.  To enable an application group for client\-side monitoring, on the **Enable Client\-Side Monitoring** page, select the application you want to enable for client\-side monitoring. To customize settings for a selected application component, click **Customize**.

5.  On the  **Modifying Settings** page, you can configure the same settings for the application component that you did for the entire application group with the addition of **Excluded pages** and **Transactions**. In the **Excluded Pages** section, click **Add** to add the pages that you want to exclude from client\-side monitoring. The pages you add to this list are the pages that the Check Client Side Monitoring Compatibility task found incompatible when you ran the task before configuring your application for monitoring. In the **Transactions** section, click **Add** to add transactions for ASP.NET webpages.

6.  To review all of your monitoring configurations—both server\-side configurations and client\-side configurations—click the **Summary** tab. After you have reviewed the configuration, click **OK**.

    > [!TIP]
    > If you want to change any configurations, while you are on this page is a good time to do so. For example, to review or change your server\-side configuration, click the **Server\-Side Configuration** page to see that configuration. To disable client\-side monitoring, click the **Enable Client Side Monitoring** page, and clear the check box.

7.  On the **Summary** page, review your monitoring configuration for your application group. To create the monitoring template, click **Create**.

8.  After the client\-side monitoring has been configured, you receive an alert to recycle IIS on the affected servers when the client\-side monitoring settings have been applied to the server. You can use the link in the knowledge base article to recycle the IIS application pools on the server.

    > [!NOTE]
    > After you restart IIS, an application does not begin to be monitored until it is used.

### <a name="BKMK_AddCSM"></a>To add client\-side monitoring to an existing .NET Application Performance Monitoring template

1.  To enable client\-side application monitoring to an existing **.NET Application Performance Monitoring** template, in the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, expand **Management Pack Templates**, click **.NET Application Performance Monitoring**, right\-click the application group you configured for server\-side monitoring, and then select **Properties**.

2.  On the **Properties** page, click the **Enable Client Side Monitoring** tab, and select the **Enable** check box next to the application group.

    **Enable client\-side monitoring**

    ![](../Image/AppMonitoring_AuthConfig2.gif)

3.  The **Customize** option on this page opens the  **Modifying Settings** page as described in the previous procedure.

4.  To configure client\-side default settings, click the **Client\-Side Defaults** tab. These settings and those on the **Advanced Settings** page are described in the above procedure.

    > [!TIP]
    > Only applications hosted on servers that are members of both the server\-side and client\-side targeted groups are monitored by client\-side monitoring.

5.  To review all of your monitoring configurations—both server\-side configurations and client\-side configurations—click the **Summary** tab. After you have reviewed the configuration, click **OK**.

6.  On the **Summary** page, review your monitoring configuration for your application group. To create the monitoring template, click **Create**.

7.  After the client\-side monitoring has been configured, you receive an alert to recycle IIS on the affected servers when the client\-side monitoring settings have been applied to the server. You can use the link in the knowledge base article to recycle the IIS application pools on the server.

    > [!NOTE]
    > After you restart IIS, an application does not begin to be monitored until it is used.

## See Also
[Before You Begin Monitoring .NET Applications](../Topic/Before-You-Begin-Monitoring-.NET-Applications.md)
[How to Start Monitoring a New Application](../Topic/How-to-Start-Monitoring-a-New-Application.md)
[Authoring Strategies for .NET Application Monitoring](../Topic/Authoring-Strategies-for-.NET-Application-Monitoring.md)

