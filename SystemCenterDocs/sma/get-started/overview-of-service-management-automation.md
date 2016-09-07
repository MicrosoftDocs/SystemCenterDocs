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

## What"s in Service Management Automation?
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
In System Center 2016, the Orchestrator component enables you to automate business processes and IT operations in your data center without scripting or programming. Orchestrator is a feature in System Center 2016. If you already have System Center 2016 installed, and you do not plan to install Windows Azure Pack, use Orchestrator.

Service Management Automation in Windows Azure Pack enables you to automate processes within the Windows Azure Pack. Because Service Management Automation runs Windows PowerShell, you can also use Windows PowerShell cmdlets to run other System Center 2016 components, including Orchestrator. If you are planning to use the Windows Azure Pack, use Service Management Automation, and then you can continue to leverage your System Center 2016 installation (if one exists).

> [!IMPORTANT]
> The [Service Management Automation Developer's Guide](http://go.microsoft.com/fwlink/?LinkId=398741) is now available. This is a set of REST API reference documentation for the Service Management Automation web service.
