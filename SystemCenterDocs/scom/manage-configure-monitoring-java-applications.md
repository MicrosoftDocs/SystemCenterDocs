---
title: How to Configure Monitoring for Java Applications
description: This article describes how to configure monitoring of Java applications with Operations Manager.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 06/20/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
ms.assetid: ec45bdd7-cc61-4c81-8d1c-a4aae303f892
---

# How to Configure Monitoring for Java applications
Getting started with monitoring Java applications requires these four general steps:  
  
1.  Import and configure the Management Pack for Java Enterprise Edition (JEE)    
  
2.  Import the Management Pack for Java Application Performance Monitoring  
  
3.  Manually deploy the Java Application Performance Monitoring Agent  
  
4.  Verify the Java Application Performance Monitoring Agent deployment  
  
## Import and configure the management pack for Java Enterprise Edition   
  
1.  Import and configure the Management Pack for Java Enterprise Edition (JEE), including installation of BeanSpy application. Java Application Performance Monitoring will not work without the JEE management pack configured and BeanSpy installed.  
  
    > [!IMPORTANT]  
    > Although the Management Pack for JEE supports several types of application servers, Java Application Monitoring only supports Tomcat.  
  
    Download the Management Pack for JEE and the Management Pack Guide for JEE. This management pack monitors JEE application servers and is available for IBM WebSphere, Oracle WebLogic, Red Hat JBoss, and Apache Tomcat. Go to the [System Center Management Pack for Java Enterprise Edition (JEE) on the Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44576), click **Download**, and then select the files you want to download. For example, select the management pack (SC2012OM_JEE_MP.msi) and select the Management Pack Guide for Tomcat (OpsMgr_MP_Tomcat.docx).  
  
    > [!IMPORTANT]  
    > Make sure to download the corresponding management pack guide (.docx file) for the application server you are using. It contains the details of how to install the management pack and describes what is monitored.  
  
    The System Center Management Pack for Tomcat, for example, allows an IT administrator to monitor the health of JEE application server instances in Operations Manager. In addition, it provides the option to deploy BeanSpy, an open source technology from Microsoft, that provides deeper monitoring, which includes memory usage.  
  
2.  After the management packs for the JEE application servers are imported, the instances of Tomcat application servers will be automatically discovered. The discovery interval is set to 4 hours by default, so discovery can take up to that length of time. On Tomcat, an application server must be running for Operations Manager to discover it for the first time. After an instance of an application is discovered, the configuration is removed only when the application server is uninstalled.  
  
    To monitor instances of the Tomcat Application Server, in the Operations console, click **Monitoring**, expand **Application Monitoring**, **expand Java Monitoring**, expand **JEE Application Servers**, expand **Tomcat Application Server**, and then select the monitoring folder you want. For details, see the Management Pack Guide for Tomcat or the management pack guide for JEE monitoring that you chose to download.  
  
3.  Follow the procedure to deploy BeanSpy to an application server. BeanSpy is an open source technology from Microsoft that relies on Java Management Extension (JMX) to enable the monitoring pack to get detailed information from the application server instances.  
  
4.  Using instructions in the Management Pack Guide for JEE, follow the procedure to enable deep monitoring mode.  
  
### Import the management pack for Java Application Performance Monitoring  
  
1.  Now that the Management Pack for Java Enterprise Edition is imported and configured and BeanSpy deployed, import the Management Pack for Java Application Performance Monitoring. Download the management pack from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=313918).  
  
2.  The Management Pack for Java Application Performance Monitoring (JavaAPMManagementPack.msi) contains these files:  
  
    -   Microsoft.JEE.APM.Library.mpb  
  
    -   Microsoft.JEE.Tomcat.APM.Library.mp  
  
    -   Microsoft.JEE.Tomcat.5.Apm.mp  
  
    -   Microsoft.JEE.Tomcat.6.Apm.mp  
  
    -   Microsoft.JEE.Tomcat.7.Apm.mp  
  
    Import these library management packs:  
  
    -   Microsoft.JEE.APM.Library.mpb  
  
    -   Microsoft.JEE.Tomcat.APM.Library.mp  
  
3.  Import the management packs for the versions of the Tomcat application servers that you are monitoring.  
  
    -   Microsoft.JEE.Tomcat.5.Apm.mp  
  
    -   Microsoft.JEE.Tomcat.6.Apm.mp  
  
    -   Microsoft.JEE.Tomcat.7.Apm.mp  
  
### Manually deploy the Java Application Performance Monitoring agent and enable Java Application Performance Monitoring  
  
1.  Now that you have configured the Management Pack for Java Enterprise Edition (JEE) through deep monitoring and imported the Management Pack for Java Application Performance Monitoring, you are ready to manually deploy the Java Application Performance Monitoring agent. To see application servers you have configured for monitoring, in **Monitoring**, click **Configurations**.  
  
2.  To enable Java Application Performance Monitoring, in the **Monitoring** pane, in the **Tasks** pane, click **Deep Monitored Configurations**, and then select a deep monitoring application server.  
  
3.  After you select an application server to enable Java Application Performance Monitoring on, in the **Tasks** pane, in **Monitored application server instance Tasks**, click **Extract APM Jar files**. This extracts the Java agent files to either the monitored machine (when a server is running Windows), or to the gateway or management server (when a server is running Linux). The Task output tells you which machine the files have been extracted to and where they were extracted. For more information, see the [Management Pack Guide for Java Application Performance Monitoring](http://technet.microsoft.com/en-us/library/dn502605.aspx).  
  
4.  Next, reconfigure the Java application server. To enable Java Application Performance Monitoring, specify command line options that use Jar file as class loader and then restart the application. Another discovery after you install the agent enables Application Performance Monitoring.  
  
### Verify Application Performance Monitoring agent deployment and override monitors  
  
1.  To verify if Application Performance Monitoring is monitoring an application, right click an application and you can see a list of counters: Monitored Requests/sec, Average Request Time, Performance Events/sec, Exception Events/sec, and, importantly, values for each counter. Five monitors apply to these. For more information about monitors, see the [Management Pack Guide for Java Application Performance Monitoring](http://technet.microsoft.com/en-us/library/dn502605.aspx).  
  
    > [!IMPORTANT]  
    > If you do not see values for the counters, Application Performance Monitoring is not enabled for these applications. This means that you might need to wait for Application Performance Monitoring discovery.  
  
2.  To see monitors, in Health Explorer, right-click an application, click **Open**, and then click **Performance View**. Some monitors some are disabled.  
  
3.  To override monitors, in Health Explorer, right-click a monitor and click **Monitor properties**. On the monitor's **Properties page**, click **Overrides** tab, click **Override** and then select the rule you want to override. On the **Override Properties page** you can enable/disable monitors and change the monitor threshold settings.  
  
### View events using Application Diagnostics  
  
Like .NET Application Performance Monitoring, you can use Application Diagnostics to view event information for Java Application Performance Monitoring. For information about opening and using Application Diagnostics, see [Working with the Application Diagnostics Console](manage-working-with-the-application-diagnostics-console.md) and [Working with Events by Using Application Diagnostics](manage-working-with-events-using-application-diagnostics.md).  
  
Due to the way Java statistics are reported, some of the standard Application Performance Monitoring reports do not apply to Java Application Performance Monitoring. For instance, you might see **NA** in some of the report columns where Java Application Performance Monitoring does not apply. Additionally, due to the way that Java application containers map to servers, many server-level reports do not have data.  
  