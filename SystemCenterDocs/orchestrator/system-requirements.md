---
ms.assetid: 46cc3ac5-8ed0-4007-a35b-cf13d04a2806
title: System Requirements for System Center 2016 - Orchestrator
description: The system requirements article provides general performance and scalability guidance for consideration as part of your design planning of your Orchestrator deployment.
ms.author: CFreeman
manager: CarmonM
ms.date: 1/4/2017
ms.custom: na
author: CFreemanwa
ms.prod: system-center-threshold
ms.technology: Orchestrator
ms.topic: article
---

# System requirements for System Center 2016 - Orchestrator

>Applies To: System Center 2016 - Orchestrator

The topic describes general performance and scalability guidance for System Center 2016 - Orchestrator and recommends hardware configurations for a variety of workloads. Because System Center 2016 is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.

## Hardware

| Orchestrator Server Role | x64 Processor (min) | Memory (min) | Disk space (min) |
|:-----|:----|:---- |:---- |
|All server roles|2.1 GHz, dual-core CPU |2 GB|200 MB

## Server operating system

The following versions of Windows Server operating system are supported.

| Component | Windows Server 2012 R2 Standard, Datacenter | Windows Server 2016 Standard, Datacenter with Desktop Experience | Windows Server Core 2016 |
|:--- |:---|:--- |:--- |
|All server roles|Supported|Supported|Not Supported


## Client operating system

The following versions of Windows client operating system are supported for the Orchestrator.

|Component| Windows 7 | Windows 8 | Windows 8.1 | Windows 10 Enterprise |
|:--- |:---|:--- |:--- |:---|
|Runbook Designer|Not supported|Not Supported|Not Supported|Supported

## SQL Server support

|Component|SQL Server 2012 SP2 Enterprise, Standard (64 bit)|SQL Server 2014 Enterprise, Standard (64-bit)|SQL Server 2014 SP1 Enterprise, Standard (64-bit)|SQL Server 2014 SP2 Enterprise, Standard (64-bit)|SQL Server 2016, Enterprise, Standard (64-bit)|
|:--- |:---|:--- |:--- |:---|:---|
|Management Server|Supported|Supported|Supported|Supported|Supported|

## .Net requirements

All Orchestrator server roles require .Net 3.5 SP1 in order to run the setup program. The Orchestrator Web Service requires .Net 4.5 with WCF Activation.

You can download .Net 3.5 SP1 at:  

### To turn on WCF activation

1. On the Windows Start screen, click the **Server Manager** tile.
2.	On the **Manage** menu in the Server Manager console, click **Add Roles and Features**.
3.	Go through the wizard until you reach the **Features** page.
4.	Expand **.NET Framework 4.5 Features**.
5.	Select **.NET Framework 4.5** if it isn’t already selected.
6.	Expand **WCF Services**.
7.	Select **HTTP Activation** if it isn’t already selected.
8.	Click **Next** and follow the prompts to finish the installation. If you have problems, check the issues covered in [Troubleshoot Your Orchestrator Installation](https://technet.microsoft.com/en-us/library/hh546549.aspx).


## Virtualization

Deploying and running Orchestrator on a virtualized operating system is fully supported. The software requirements are the same as those listed above. Any of the Orchestrator roles can also be run on a virtualized server running in Microsoft Azure.

## Next steps
[Install Orchestrator](install.md)
