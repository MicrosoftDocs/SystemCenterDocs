---
title:  Overview of Service Management Automation
description: Service Management Automation is used to construct, run, and manage runbooks to integrate, orchestrate, and automate IT business processes.
manager:  carmonm
ms.topic:  article
author:  rayne-wiselman
ms.author: raynew
ms.prod:  system-center-threshold
ms.date: 05/08/2018
ms.technology:  service-management-automation

---

# Overview of Service Management Automation

Service Management Automation (SMA) is a set of tools that is integrated as the SMA extension in Windows Azure Pack for Windows Server. IT pros and IT developers can use SMA to construct, run, and manage runbooks to integrate, orchestrate, and automate IT business processes. SMA runbooks run on the Windows PowerShell engine.



## SMA components
SMA uses the following three underlying components, that are connected to Windows Azure Pack through the SMA service endpoint:

**Web service**

-   Connects to Windows Azure Pack

-   Distributes runbook jobs to runbook workers

-   Supports HTTPS

-   Enables security group to control access

**Runbook worker**

-   Executes runbook jobs

-   Runs under a service account

**PowerShell module**

-   Enables SMA management by using Windows PowerShell cmdlets

### Should I use SMA or System Center - Orchestrator?

The System Center - Orchestrator component enables you to automate business processes and IT operations in your data center without scripting or programming. If you prefer a graphical authoring approach, use Orchestrator.

SMA enables you to automate business processes and IT operations via PowerShell. With the support for the latest PowerShell features, you can use SMA to automate the management of any software that provides PowerShell cmdlets including other System Center components (even Orchestrator). If you would like to automate via PowerShell, use Service Management Automation to manage your all your automation from a single place.

SMA also has deep integration with Windows Azure Pack, however, you no longer need to use Windows Azure Pack portal for authoring SMA runbooks. Authoring can be done within PowerShell ISE through [PowerShell ISE Add-on](https://www.powershellgallery.com/packages/SMAAuthoringToolkit/). SMA now also supports native PowerShell script type runbooks. You can know more about the new features in SMA over [here](whats-new-in-service-management-automation.md)

The following diagram illustrates each of the SMA features, and the communication with a Windows Azure Pack installation.

![SMA Architecture diagram](/system-center/sma/media/overview-of-service-management-automation/smaarchitecture.png)


-   The SMA web service communicates with Windows Azure Pack, and authenticates users.

-   The SQL Server databases store and retrieve runbooks, runbook assets, activities, integration modules, and runbook job information.

-   Runbook workers run the runbooks, and they can be used for load balancing.

-   The management portal in Windows Azure Pack is where you author, debug, and start and stop runbooks.

> [!IMPORTANT]
> The [SMA Developer's Guide](https://go.microsoft.com/fwlink/?LinkId=398741) is now available. This guide is a set of REST API reference documentation for the SMA web service.

## Next steps

Learn how [SMA executes runbooks](runbook-automation.md)
