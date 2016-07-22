---
title: Notes for AVIcode 5.7 Customers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85334e43-8bce-45a3-bbe2-0bc483e71561
author:mgoedtel
manager:cfreemanwa
---
# Notes for AVIcode 5.7 Customers
[!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] includes application monitoring. The major difference is that [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] required you to deploy a separate infrastructure alongside [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)]. Now these infrastructures have been combined, so you don't need to install anything.  
  
> [!NOTE]  
> Now that [!INCLUDE[sc2012](../../om/manage/includes/sc2012_md.md)] is generally available as of April 17, 2012, [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] will no longer be available as a standalone product from the Microsoft AVIcode subsidiary. [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] support will continue for 12 months following general availability of [!INCLUDE[sc2012](../../om/manage/includes/sc2012_md.md)]. If certain customers already have existing support agreements with other support terms, those agreements will be honored until they expire. When the support for [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] ends, the Microsoft AVIcode subsidiary will no longer provide new updates or hotfixes for [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] and we will encourage customers to move to [!INCLUDE[sc2012](../../om/manage/includes/sc2012_md.md)], which will be supported as described in the [Microsoft Support Lifecycle Policy FAQ](http://go.microsoft.com/fwlink/?LinkId=251881)  
  
If you are running [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] to monitor applications and install [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], servers that have [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] agents installed will continue to work in the same way they were doing before since only [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] has been upgraded. NET Application Performance Monitoring configuration will not affect the [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] agents because they will not receive it. If you have legacy applications monitored by [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] \(IIS6, .NET services, SharePoint 2007, for example\), you can continue to monitor them with [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)]. You can begin using .NET Application Performance Monitoring on new servers where [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] has not been installed or was removed.  
  
## Converting [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] Monitoring to .NET Application Performance Monitoring  
As a legacy product, [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] will receive very limited updates. Future technologies will only be added to .NET Application Performance Monitoring in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)].  
  
When you are ready to move from using [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] to .NET Application Performance Monitoring to monitor applications \(for example, when [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] is monitoring IIS7 already or when Windows is upgraded\), you can:  
  
-   Uninstall [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] agent from that computer.  
  
-   Repair install the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agent, which will install the Application Performance Monitoring service.  
  
-   Manually reconfigure .NET Application Performance Monitoring for the application running on IIS7 with similar settings that you were using previously with [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)]. For more information, see [.NET Application Performance Monitoring Template](http://go.microsoft.com/fwlink/?LinkId=230647).  
  
## Continuing to Use [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] with [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)]  
Features of [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] and .NET Application Performance Monitoring can generally co\-exist, but some cannot. For example, the [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] SEViewer and the new Application Diagnostics cannot be installed on the same system. You can use both consoles in the same environment, but they must be installed on separate IIS hosts.  
  
When monitoring applications using both [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] and .NET Application Performance Monitoring in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], data is shown in the respective monitoring views. For [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)], data continues to flow through SELog and SEViewer. For .NET Application Performance Monitoring in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], monitoring data is viewed in Application Diagnostics.  
  
### Supported AVIcode Versions  
Only [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] when integrated with [!INCLUDE[om2007r2short](../../om/manage/includes/om2007r2short_md.md)] with the latest cumulative updates is supported. Previous AVIcode versions are not supported. [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] functionality has not been enhanced. The [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] configurations you have been using to monitor applications have not been converted to .NET Application Performance Monitoring configurations. When upgrading from [!INCLUDE[om2007r2short](../../om/manage/includes/om2007r2short_md.md)] to [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], you need to manually import new [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] management packs. For more information, see [Steps to import AVIcode 5.7 templates after upgrading](http://go.microsoft.com/fwlink/?LinkID=230859).  
  
### How Upgrade Works with [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] Agents and .NET Application Performance Monitoring Agents  
Upgrading to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] behaves this way:  
  
-   Upgrading to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] is not blocked because [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] agents are present. When an [!INCLUDE[om2007r2short](../../om/manage/includes/om2007r2short_md.md)] agent and an [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] agent are found, the upgrade to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] proceeds, but the .NET Application Performance Monitoring service is not installed. The [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] service is left instead.  
  
    > [!IMPORTANT]  
    > You cannot have the [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] service installed on the management servers. In this case, you will need to remove the [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] service before upgrading.  
  
-   When [!INCLUDE[om2007r2short](../../om/manage/includes/om2007r2short_md.md)] agents are found without [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] on the system, the upgrade to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] proceeds and the .NET Application Performance Monitoring agent is installed.  
  
-   If .NET Application Performance Monitoring has already been deployed and you try to install [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] on it, this is blocked through the push install. If you manually force it, you could succeed, but the agents will conflict with one another and neither will work correctly. There it is a monitor that targets activated Application Performance Monitoring agents that will put the agent into a warning state if both the [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] and the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] Application Performance Monitoring agents are on the same server.  
  
-   If you are using [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] and do not want to install .NET Application Performance Monitoring on your agent\-managed computers, use the \/NOAPM\=1 agent manual install command line switch to prevent .NET Application Performance Monitoring from being installed. This leaves the AVIcode agent in place. For more information, see [Install Agent Using the Command Line](../Topic/Install%20Agent%20Using%20the%20Command%20Line.md).  
  
> [!NOTE]  
> There is a monitor named AVIcode Intercept Service found that targets the Agent class in [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] that is disabled by default, but can be enabled to monitor for the AVIcode agents on systems where the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agent is present alongside the [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] service.  
  
### Manually Importing [!INCLUDE[avicode57](../../om/manage/includes/avicode57_md.md)] Management Packs  
When the AVIcode.NET Enterprise Management Pack for Operations Manager 2007 is present in the management group, Setup will continue, but some management packs will need to be manually upgraded after setup has finished fixing incompatibilities with [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)]. The management pack files are in the \/SupportTools directory on the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] media. They are not imported automatically.  
  
The management packs that need to be imported are:  
  
-   AVIcode.DotNet.SystemCenter.Enterprise.Monitoring.mpb  
  
-   AVIcode.DotNet.SystemCenter.Client.Monitoring.mp  
  
