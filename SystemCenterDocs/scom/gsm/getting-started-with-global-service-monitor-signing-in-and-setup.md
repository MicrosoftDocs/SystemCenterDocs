---
title: "Getting Started with Global Service Monitor: Signing In and Setup | Microsoft Docs"
ms.custom: ""
ms.date: 4/26/2018
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.tgt_pltfrm: ""
ms.topic: article
applies_to: System Center 2016 - Operations Manager
ms.assetid: 15971a66-8e19-4ddb-8b98-8ac8c8c9d7a1
author: mgoedtel
ms.author: magoedte
manager: carmonm
---
# Getting Started with Global Service Monitor: Signing In and Setup
Getting started with [!INCLUDE[gsmlong](../includes/gsmlong-md.md)] involves several steps. These include signing up for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], setting up [!INCLUDE[om12long](../includes/om12long-md.md)], and importing the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] management packs.  
  
### Before You Begin  
  
1.  Install [!INCLUDE[om12short](../includes/om12short-md.md)]. You can install [!INCLUDE[om12short](../includes/om12short-md.md)] on a single server. If you want to run tests from internal locations, you will also need to install agents (watchers).  
  
    -   Make sure that the servers in the management server pool you choose for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] communication have access to the Internet. To use [!INCLUDE[gsmshort](../includes/gsmshort-md.md)], your management pool needs http: access to the Internet so that the pool can communicate with the monitoring agents running in the cloud. These agents are automatically discovered when you sign up for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)]—you do not have to deploy them in a separate step.  
  
        > [!IMPORTANT]
        >  Communication with the cloud is always initiated by your on-premise management group.  
  
        > [!NOTE]
        >  [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] agent discovery turns management servers that are not part of the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] management server pool to an error state. To mitigate this, turn off alerting or disable the System Center Management Health Service Credentials Not Found monitor. If you turn off alerting, the monitor state will remain red. If you disable the monitor, the state of the Management Server will turn green. Note that disabling the monitor will disable all alerting and monitoring on the distribution of all of the Run As accounts.  
  
    -   Make sure Windows Identity Foundation is installed on your management server that is communicating with the cloud and everywhere the [!INCLUDE[om12short](../includes/om12short-md.md)] console is installed. Windows Identity Foundation is required. If you do not have it installed, go to the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=224157), download Windows Identity Foundation, and then install it.  
  
        > [!IMPORTANT]
        >  After you install Windows Identity Foundation, you must restart the health service.  
  
        > [!IMPORTANT]
        >  If you import the management packs before you install Windows Identity Foundation, when you install Windows Identity Foundation, the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] landing page indicates that you can configure tests. However, the next step is to sign up. You cannot configure tests until you sign up for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)].  
  
## Sign Up  
  
#### To sign up for [!INCLUDE[gsmshort](../includes/gsmshort-md.md)]  
  
1.  Download and then import all of the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] management packs from this site [GSM Management Packs](https://www.microsoft.com/en-us/download/details.aspx?id=36422).  
  
    > [!NOTE]
    >  If you want to download [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] web test results and have them attached to alerts so that you can more easily give the test results to your engineering team, you also have to install the Alert Attachment management pack. Additionally, to better integrate this with your Development and Operations (DevOps) processes, you can synchronize these alerts and their attached web test results with Team Foundation Server (TFS) work items by downloading the TFS Work Item Synchronization management pack. If you are using [!INCLUDE[sc2012r2_1](../includes/sc2012r2-1-md.md)], see [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 R2](http://go.microsoft.com/fwlink/?LinkId=307114) and [How to Configure Integration with TFS in System Center 2012 R2](http://go.microsoft.com/fwlink/?LinkId=307113). If you are using [!INCLUDE[sc2012sp1_short](../includes/sc2012sp1-short-md.md)], see [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=275127) and [How to Configure Integration with TFS in System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=275126).  
  
2.  In the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Administration**, and then click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**. This is the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] landing page that you can use as the hub for your work with [!INCLUDE[gsmshort](../includes/gsmshort-md.md)].  
  
3.  On the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] landing page, click **Start Subscription**.  
  
4.  On the **Subscription Credentials** page, login with  a valid Microsoft Account.  
  
5.  On the **Component Configuration** page, designate a resource pool. Using a pool of management servers to monitor your tests gives you highly available communication with the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] service. If one member of the pool becomes unavailable, another one takes over, whereas when a single server becomes unavailable, your system cannot communicate with the service. Note: If you use a management pool, it is a best practice to define your own [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] management pool instead of using the default **All management server** pool. Agent pools are not available.  
  
    > [!IMPORTANT]
    >  Each member of the pool must have Windows Identity Foundation installed and must have Internet access.  
  
     You can also use a proxy server to connect to [!INCLUDE[gsmshort](../includes/gsmshort-md.md)]. Select **User Proxy server to connect** and then specify the address of the proxy server by using this syntax: http://\<proxyserveraddress>:\<port>.  
  
    > [!NOTE]
    >  Specify a proxy server for the resource pool only if one is required in your environment. If the proxy server requires authentication, create or add the required Run As account to the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] Run As profile.  
  
6.  To view the **Summary** page, click **Next**. When you have confirmed your settings, click **Start Subscription**.  
  
7.  On the **Completion** page, click **Finish** to close the setup wizard.  
  
8.  You are now ready to use [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] to configure tests.  
  
> [!NOTE]
>  If, during setup, you see a message titled **Could not upload a certificate to [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] Online Service**, or if you receive an authentication failed error, check to make sure the proxy settings are not blocking access to the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] service.  
  
> [!NOTE]
>  You can end your subscription at any time. Go to the [!INCLUDE[gsmshort](../includes/gsmshort-md.md)] landing page and then click **Stop Subscription**. If you have lots of templates defined, deleting the external tests while you are deactivating your subscription could take 15 minutes or more.