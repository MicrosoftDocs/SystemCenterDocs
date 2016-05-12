---
title: Monitoring SharePoint 2010 Applications in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0df0d71-721d-4055-afc7-bd670099f27e
---
# Monitoring SharePoint 2010 Applications in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](Token/sc2012sp1notetopic_md.md)]

SharePoint application technologies provide various extensibility and customization mechanisms. Custom application code running in SharePoint environment can extend or replace standard pages, can implement custom business rules, often integrates with third\-party components, and custom solutions written to operate using SharePoint framework. The customizations and code errors in custom components can affect server performance, significantly impacting overall application experience.

[!INCLUDE[om12short](Token/om12short_md.md)] lets you monitor SharePoint 2010 web front\-end components. You can monitor standard and custom SharePoint webpages for performance degradation and server\-side exceptions.

> [!WARNING]
> Client\-side .NET Application Performance Monitoring \(APM\) is not supported for SharePoint. Enabling client\-side .NET Application Performance Monitoring for SharePoint can result in unpredictable application behavior and failures.

## Monitoring for SharePoint Applications
SharePoint web front\-end components are natively discovered by the IIS management pack as endpoints. You can enable monitoring for SharePoint applications in much the same way you enable monitoring for other .NET web applications. Use the .NET Application Performance Monitoring template to configure SharePoint application monitoring. For more information, see [.NET Application Performance Monitoring Template](.NET-Application-Performance-Monitoring-Template.md).

When monitoring SharePoint applications for performance violations, events in Application Diagnostics contain additional information, such as **SharePoint server API calls** and **Web Part calls**. For each API call, the APM agent will collect relevant SharePoint methods parameters. The APM agent also tracks the execution time for the slowest calls. When detecting performance issues from standard SharePoint webpages using web parts, the slowest resource calls are shown and poorly performing web part names are collected next to the location of the web part on the SharePoint page. When detecting performance issues from custom SharePoint webpages, only the SharePoint API calls are shown.

When monitoring SharePoint applications for exceptions, the exception call stack contains the relevant SharePoint specific parameters available for troubleshooting.


