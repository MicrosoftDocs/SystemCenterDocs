---
title: Monitoring Web Applications with Microsoft Monitoring Agent
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bdf8f8b7-8f6b-436d-a464-f9681b15cc61
author:mgoedtel
manager:cfreemanwa
---
# Monitoring Web Applications with Microsoft Monitoring Agent
When Microsoft Monitoring agent is used together with System Center [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], it adds value for IT Operations by providing real\-time alerting, operational reporting, and centralized management of configuration. Microsoft Monitoring Agent without connection to System Center can be used as a lightweight Application Performance Monitoring \(APM\) solution for Microsoft .NET Framework applications that does not require heavy infrastructure from IT Operations, so you can begin monitoring applications within a few minutes.  
  
You can download Microsoft Monitoring Agent for stand\-alone use or for use with [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] from the Microsoft Download Center. You can also install it from the [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] media. Downloading Microsoft Monitoring Agent from the Download Center gives you the latest version of the agent with the latest monitoring capabilities. After you install Microsoft Monitoring Agent for use without [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], you can use it to collect application traces locally. Microsoft Monitoring Agent adds the following new Windows PowerShell commands that control local monitoring:  
  
-   **Start\-WebApplicationMonitoring** starts monitoring an Internet Information Services \(IIS\) web application.  
  
-   **Stop\-WebApplicationMonitoring** stops monitoring an IIS web application and creates a Microsoft IntelliTrace file by using data that is collected during monitoring.  
  
-   **Checkpoint\-WebApplicationMonitoring** creates a snapshot of the IntelliTrace file and continues monitoring.  
  
-   **Get\-WebApplicationMonitoringStatus** gets the monitoring status of all monitored web applications.  
  
## Monitoring by Using Local Collection  
  
#### To start and stop monitoring by using local collection  
  
1.  Start Windows PowerShell as an administrator. Your account must be a member of the Local Administrators group to perform this task, or you must run Windows PowerShell as a user who belongs to the Local Administrators group.  
  
2.  If you are using Windows PowerShell&nbsp;2.0, you must manually import the monitoring module Microsoft.MonitoringAgent.PowerShell.dll from the Microsoft Monitoring Agent installation location. By default, the module is located at C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\PowerShell\\Microsoft.MonitoringAgent.PowerShell\\. For example, to import the module, at the Windows PowerShell command prompt, type `import-module "C:\Program Files\Microsoft Monitoring Agent\Agent\PowerShell\Microsoft.MonitoringAgent.PowerShell\Microsoft.MonitoringAgent.PowerShell.dll".`  
  
    > [!IMPORTANT]  
    > If you are using Windows PowerShell&nbsp;2.0 and close Windows PowerShell, you must repeat this step to use any Windows PowerShell commands in Microsoft Monitoring Agent.  
  
    If you are using Windows PowerShell&nbsp;3.0, the module will already be imported and you do not need to import it manually as described in this step.  
  
3.  At the Windows PowerShell command prompt, type `Start-WebApplicationMonitoring` and then specify the web application name, the monitoring mode, and the output location. For example, type `Start-WebApplicationMonitoring Fabrikam/FabrikanFiber.Web Monitor c:\outputlogs`.  
  
    -   To find the web application name, use the **Get\-WebSite** and **Get\-WebApplication** Windows PowerShell commands.  
  
    -   To limit the amount of space that is allocated for traces, use the *MaximumFileSizeInMegabytes* parameter and allocate enough space.  
  
    -   The monitoring mode can be Trace, Monitor, or Custom. These monitoring modes use a *collection plan*, which determines how an application is monitored \(such as custom namespaces to monitor, all or only critical exceptions, and application\-specific exception handlers\). When you use Trace, you can use Microsoft Monitoring Agent in the same way that you might have used an IntelliTrace collector, and you can use collection plans in the form of the IntelliTrace collector that was part of Microsoft Visual Studio&nbsp;2010 and Visual Studio&nbsp;2012 and is available in Visual Studio&nbsp;2013. The Monitor option uses the default monitoring collection plan that is preconfigured with Microsoft Monitoring Agent. The default collection plan is located in the same folder as the monitoring module. You can use this default collection plan by using the Monitor option, or you can copy it to a different file and customize it and use it with the Custom monitoring mode.  
  
    > [!WARNING]  
    > Starting and stopping monitoring might restart or recycle your application IIS pool.  
  
4.  To stop monitoring, type `Stop-WebApplicationMonitoring`. For example, type `Stop-WebApplicationMonitoring Fabrikam\FabrikamFiber.Web`. For more information about using Windows PowerShell commands, see these Windows PowerShell topics: [Microsoft.MonitoringAgent.PowerShell.Start\-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313686), [Microsoft.MonitoringAgent.PowerShell.Stop\-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313687), [Microsoft.MonitoringAgent.PowerShell.Checkpoint\-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313684), [Microsoft.MonitoringAgent.PowerShell.Get\-WebApplicationMonitoringStatus](http://go.microsoft.com/fwlink/?LinkID=313685).  
  
5.  To learn more, see [Monitor your app with Microsoft Monitoring Agent](http://go.microsoft.com/fwlink/?LinkId=324046).  
  
## Using Local Monitoring and the .NET APM Template in System Center at the Same Time  
If you configured application monitoring by using the .NET Application Performance Monitoring template in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], you can still use Windows PowerShell commands in Microsoft Monitoring Agent local monitoring to monitor applications. The Windows PowerShell commands in Microsoft Monitoring Agent have higher priority than the APM monitoring configuration and will temporarily override the APM monitoring configuration when you use them to start local collection. For more information, see [Microsoft Monitoring Agent Requirements and Compatibility](../../om/manage/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md).  
  
## Customizing Local Collection  
To get useful results from your monitoring, you might need to customize default collection settings, such as namespaces and thresholds that specify your application\-specific service level agreements \(SLAs\). This customization is controlled in your collection plan. After you edit the collection plan, you must restart monitoring.  
  
