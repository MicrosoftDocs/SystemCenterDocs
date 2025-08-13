---
description: include file to describe the minimum hardware and software configurations that are required for a full installation of Service Management Automation 2016.
ms.topic:  include
author: jyothisuri
ms.author: jsuri
ms.service:  system-center
keywords:  
ms.date: 08/07/2025
title:  include file
ms.subservice:  service-management-automation
ms.assetid: 57ba1e98-2460-4a21-b083-9f77f16e4890
---

## System requirements for Service Management Automation 2016

The following sections describe the minimum hardware and software configurations that are required for a full installation of Service Management Automation in System Center 2016.

## Hardware requirements
The following recommended configurations should be used:

|Performance component|Recommendation|
|-------------------------|------------------|
|Virtual machines|Three, each with a runbook worker and web service installed<br /><br />Load-balanced incoming traffic<br /><br />Minimum of two cores and 4 GB of RAM for each virtual machine<br /><br />60 GB of available disk space|
|SQL Server|One computer with 8 GB of RAM and eight cores **Note:** One month of data under heavy load (12 jobs per minute for a month) results in 20 GB of disk space usage. Job purging should be used to keep this usage from growing beyond this amount.|

## Software requirements
The following software must be installed for each role:

|Role|Prerequisites|
|--------|-----------------|
|Runbook worker|Windows Server 2012 R2 or above<br /><br />Windows PowerShell 4.0 or above|
|Automation web service|Windows Server 2012 R2 or above<br /><br /> SQL Server 2012 SP4 (minimum) <br /><br /> **Note**: Supports SQL 2012, 2014, and 2016 service packs that are in support by Microsoft. Here are the [supported service packs for 2012](/lifecycle/products/?terms=SQL+Server+2012), [2014](/lifecycle/products/?terms=SQL+Server+2014), and [2016](/lifecycle/products/?terms=SQL+Server+2016). <br /><br />Internet Information Services (IIS) 7.5 or above (hosts the web service)<br /><br />IIS Basic Authentication<br /><br />IIS Windows Authentication<br /><br />IIS URL Authorization<br /><br />ASP.NET 4.5<br /><br />.NET Framework 3.5 (for the Setup program)<br /><br />.NET Framework 4.5<br /><br />WCF HTTP Activation|
|Windows PowerShell module|Windows PowerShell 4.0 or above|


## Install .NET Framework 4.5 and HTTP Activation

Before installing the web service, use the following procedure to install .NET Framework 4.5 and HTTP Activation:


1.  On the Windows **Start** screen, select the **Server Manager** tile.

2.  On the **Manage** menu in the Server Manager console, select **Add Roles and Features**.

3.  Follow the wizard until you reach the **Features** page.

4.  Expand **.NET Framework 4.5 Features**.

5.  Select **.NET Framework 4.5** if it isn't already selected.

6.  Expand **WCF Services**.

7.  Select **HTTP Activation** if it isn't already selected.

8.  Select **Next**, and follow the prompts to finish the installation.

## Run Service Management Automation on Azure VMs
Service Management Automation runs on Microsoft Azure just as it does on physical computer systems.

Service Management Automation was tested by Microsoft by installing and using it in a Microsoft Azure virtual machine. The testing concluded that Service Management Automation was fully functional and operated exactly the same as it does on physical hardware. Stability and performance benchmarks inside a Microsoft Azure virtual machine were at a level where no special considerations were needed.

## Security requirements
The following ports must be opened for each role:

|Role|Requirement|
|--------|---------------|
|Runbook worker|None|
|Automation web service|Default value: 9090. Configurable at install time port defaults to 9090. The installation program for Service Management Automation automatically opens the web service port on the local firewall.|
|Windows PowerShell module|None|

The following certificates are required for each component:

|Role|Requirement|
|--------|---------------|
|Runbook worker|None|
|Automation web service|A certificate that can be used for Secure Sockets Layer (SSL) encryption over HTTPS. The installation program for Service Management Automation can be used to generate a self-signed certificate.|
|Windows PowerShell module|None|