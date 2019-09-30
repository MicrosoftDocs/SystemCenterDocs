---
ms.assetid: a60bdfee-1415-4b73-b009-7b2a794fc96c
title: Notes for AVIcode 5.7 Customers
description: This article provides an overview about notes for AVIcode 5.7 Customers
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 09/26/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Notes for AVIcode 5.7 Customers

System Center – Operations Manager includes application monitoring. The major difference is that AVIcode 5.7 required you to deploy a separate infrastructure alongside Operations Manager. Now these infrastructures have been combined, so you don't need to install anything.

> [!NOTE]
> Now that System Center is generally available as of April 17, 2012, AVIcode 5.7 will no longer be available as a standalone product from the Microsoft AVIcode subsidiary. AVIcode 5.7 support will continue for 12 months following general availability of System Center 2012. If certain customers already have existing support agreements with other support terms, those agreements will be honored until they expire. When the support for AVIcode 5.7 ends, the Microsoft AVIcode subsidiary will no longer provide new updates or hotfixes for AVIcode 5.7 and we will encourage customers to move to System Center 2012, which will be supported as described in the [Microsoft Support Lifecycle Policy FAQ](http://go.microsoft.com/fwlink/?linkid=251881)

If you are running AVIcode 5.7 to monitor applications and install Operations Manager, servers that have AVIcode 5.7 agents installed will continue to work in the same way they were doing before since only Operations Manager has been upgraded. NET Application Performance Monitoring configuration will not affect the AVIcode 5.7 agents because they will not receive it. If you have legacy applications monitored by AVIcode 5.7 (IIS6, .NET services, SharePoint 2007, for example), you can continue to monitor them with AVIcode 5.7. You can begin using .NET Application Performance Monitoring on new servers where AVIcode 5.7 has not been installed or was removed.

## Converting AVIcode 5.7 Monitoring to .NET Application Performance Monitoring

As a legacy product, AVIcode 5.7 will receive very limited updates. Future technologies will only be added to .NET Application Performance Monitoring in Operations Manager.

When you are ready to move from using AVIcode 5.7 to .NET Application Performance Monitoring to monitor applications (for example, when AVIcode 5.7 is monitoring IIS7 already or when Windows is upgraded), you can:

  - Uninstall AVIcode 5.7 agent from that computer.
  - Repair install the Operations Manager agent, which will install the Application Performance Monitoring service.
  - Manually reconfigure .NET Application Performance Monitoring for the application running on IIS7 with similar settings that you were using previously with AVIcode 5.7. For more information, see [.NET Application Performance Monitoring Template](net-application-performance-monitoring-template.md).

## Continuing to Use AVIcode 5.7 with System Center 2012 – Operations Manager

Features of AVIcode 5.7 and .NET Application Performance Monitoring can generally co-exist, but some cannot. For example, the AVIcode 5.7 SEViewer and the new Application Diagnostics cannot be installed on the same system. You can use both consoles in the same environment, but they must be installed on separate IIS hosts.

When monitoring applications using both AVIcode 5.7 and .NET Application Performance Monitoring in Operations Manager, data is shown in the respective monitoring views. For AVIcode 5.7, data continues to flow through SELog and SEViewer. For .NET Application Performance Monitoring in Operations Manager, monitoring data is viewed in Application Diagnostics.

## Supported AVIcode Versions

Only AVIcode 5.7 when integrated with Operations Manager 2007 R2 with the latest cumulative updates is supported. Previous AVIcode versions are not supported. AVIcode 5.7 functionality has not been enhanced. The AVIcode 5.7 configurations you have been using to monitor applications have not been converted to .NET Application Performance Monitoring configurations. When upgrading from Operations Manager 2007 R2 to System Center 2012 – Operations Manager, you need to manually import new AVIcode 5.7 management packs. For more information, see [Steps to import AVIcode 5.7 templates after upgrading](http://go.microsoft.com/fwlink/?linkid=230859).

## How Upgrade Works with AVIcode 5.7 Agents and .NET Application Performance Monitoring Agents

Upgrading to Operations Manager behaves this way:

  - Upgrading to Operations Manager is not blocked because AVIcode 5.7 agents are present. When an Operations Manager 2007 R2 agent and an AVIcode 5.7 agent are found, the upgrade to Operations Manager proceeds, but the .NET Application Performance Monitoring service is not installed. The AVIcode 5.7 service is left instead.

   > [!IMPORTANT]
   >You cannot have the AVIcode 5.7 service installed on the management servers. In this case, you will need to remove the AVIcode 5.7 service before upgrading.

  - When Operations Manager 2007 R2 agents are found without AVIcode 5.7 on the system, the upgrade to Operations Manager proceeds and the .NET Application Performance Monitoring agent is installed.
  - If .NET Application Performance Monitoring has already been deployed and you try to install AVIcode 5.7 on it, this is blocked through the push install. If you manually force it, you could succeed, but the agents will conflict with one another and neither will work correctly. There it is a monitor that targets activated Application Performance Monitoring agents that will put the agent into a warning state if both the AVIcode 5.7 and the Operations Manager Application Performance Monitoring agents are on the same server.
  - If you are using AVIcode 5.7 and do not want to install .NET Application Performance Monitoring on your agent-managed computers, use the /NOAPM=1 agent manual install command line switch to prevent .NET Application Performance Monitoring from being installed. This leaves the AVIcode agent in place. For more information, see [Install Agent Using the Command Line](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/hh230736%28v%3dsc.12%29).

> [!NOTE]
> There is a monitor named AVIcode Intercept Service found that targets the Agent class in System Center – Operations Manager that is disabled by default, but can be enabled to monitor for the AVIcode agents on systems where the Operations Manager agent is present alongside the AVIcode 5.7 service.

## Manually Importing AVIcode 5.7 Management Packs

When the AVIcode.NET Enterprise Management Pack for Operations Manager 2007 is present in the management group, Setup will continue, but some management packs will need to be manually upgraded after setup has finished fixing incompatibilities with Operations Manager. The management pack files are in the /SupportTools directory on the Operations Manager media. They are not imported automatically.

The management packs that need to be imported are:

- DotNet.SystemCenter.Enterprise.Monitoring.mpb
- DotNet.SystemCenter.Client.Monitoring.mp
