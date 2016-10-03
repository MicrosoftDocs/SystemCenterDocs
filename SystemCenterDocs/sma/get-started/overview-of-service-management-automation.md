---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-08-18
title:  Overview of Service Management Automation
ms.technology:  service-management-automation
ms.assetid:  490faacf-b798-40ea-bb6e-106e6ad7ebaf
---

# Overview of Service Management Automation

>Applies To: System Center 2016

Service Management Automation is a set of tools that is integrated as the Service Management Automation extension in Windows Azure Pack for Windows Server. IT pros and IT developers can use Service Management Automation to construct, run, and manage runbooks to integrate, orchestrate, and automate IT business processes. Service Management Automation runbooks run on the Windows PowerShell engine.

## Service Management Automation Components
Service Management Automation uses the following three underlying components that are connected to Windows Azure Pack through the Service Management Automation service endpoint:

**Web service**

-   Connects to Windows Azure Pack

-   Distributes runbook jobs to runbook workers

-   Supports HTTPS

-   Enables security group to control access

**Runbook worker**

-   Executes runbook jobs

-   Runs under a service account

**PowerShell module**

-   Enables Service Management Automation management by using Windows PowerShell cmdlets

### Should I use Service Management Automation or System Center 2016 - Orchestrator?

In System Center 2016, the Orchestrator component enables you to automate business processes and IT operations in your data center without scripting or programming. If you prefer a graphical authoring approach, use Orchestrator.

Service Management Automation(SMA) enables you to automate business processes and IT operations via PowerShell. With the support for the latest PowerShell features, you can use SMA to automate the management of any software that provides PowerShell cmdlets including other System Center 2016 components (even Orchestrator). If you would like to automate via PowerShell, use Service Management Automation to manage your all your automation from a single place.

SMA also has deep integration with Windows Azure Pack, however, you no longer need to use Windows Azure Pack portal for authoring SMA runbooks. Authoring can be done within PowerShell ISE through [PowerShell ISE Add-on](https://www.powershellgallery.com/packages/SMAAuthoringToolkit/). SMA now also supports native PowerShell script type runbooks. You can know more about the new features in SMA over [here](what-s-new-in-service-management-automation.md)

> [!IMPORTANT]
> The [Service Management Automation Developer's Guide](http://go.microsoft.com/fwlink/?LinkId=398741) is now available. This is a set of REST API reference documentation for the Service Management Automation web service.
