---
title: System requirements for Service Management Automation
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 222692ab-765c-44bd-8d50-0c0596d26a94
---
# System requirements for Service Management Automation
This topic describes the minimum hardware and software configurations that are required for a full installation of [!INCLUDE[sma_1](../Token/sma_1_md.md)].

## Hardware requirements
The following recommended configurations should be used.

|Performance component|Recommendation|
|-------------------------|------------------|
|Virtual machines|Three, each with a runbook worker and web service installed<br /><br />Load\-balanced incoming traffic<br /><br />Minimum of two cores and 4 GB of RAM for each virtual machine<br /><br />60 GB of available disk space|
|SQL Server|One computer with 8 GB of RAM and eight cores **Note:** One month of data under heavy load \(12 jobs per minute for a month\) results in 20 GB of disk space usage. Job purging should be used to keep this usage from growing beyond this amount.|

### Software requirements
The following software must be installed for each role.

|Role|Prerequisites|
|--------|-----------------|
|Runbook worker|Windows Server 2012 R2 or above<br /><br />Windows PowerShell 4.0 or above|
|Automation web service|Windows Server 2012 R2 or above<br /><br />SQL Server 2012 SP2 or above \(Standard or Enterprise\)<br /><br />Internet Information Services \(IIS\) 7.5 or above \(hosts the web service\)<br /><br />IIS Basic Authentication<br /><br />IIS Windows Authentication<br /><br />IIS URL Authorization<br /><br />ASP.NET 4.5<br /><br />.NET Framework 3.5 \(for the Setup program\)<br /><br />.NET Framework 4.5<br /><br />WCF HTTP Activation|
|Windows PowerShell module|Windows PowerShell 4.0 or above|

Before installing the web service, use the following procedure to install .NET Framework 4.5 and HTTP Activation on Windows Server 2012 R2:

##### To install .NET Framework 4.5 and HTTP Activation

1.  On the Windows **Start** screen, click the **Server Manager** tile.

2.  On the **Manage** menu in the Server Manager console, click **Add Roles and Features**.

3.  Follow the wizard until you reach the **Features** page.

4.  Expand **.NET Framework 4.5 Features**.

5.  Select **.NET Framework 4.5** if it isn’t already selected.

6.  Expand **WCF Services**.

7.  Select **HTTP Activation** if it isn’t already selected.

8.  Click **Next**, and follow the prompts to finish the installation.

### Running [!INCLUDE[sma_1](../Token/sma_1_md.md)] on Windows Azure virtual machines
[!INCLUDE[sma_1](../Token/sma_1_md.md)] runs on Windows Azure just as it does on physical computer systems.

[!INCLUDE[sma_1](../Token/sma_1_md.md)] was tested by Microsoft by installing and using it in a Windows Azure virtual machine. The testing concluded that [!INCLUDE[sma_1](../Token/sma_1_md.md)] was fully functional and operated exactly the same as it does on physical hardware. Stability and performance benchmarks inside a Windows Azure virtual machine were at a level where no special considerations were needed.

### Security Requirements
The following ports must be opened for each role.

|Role|Requirement|
|--------|---------------|
|Runbook worker|None|
|Automation web service|Default value: 9090. Configurable at install time port defaults to 9090. The installation program for [!INCLUDE[sma_1](../Token/sma_1_md.md)] automatically opens the web service port on the local firewall.|
|Windows PowerShell module|None|

The following certificates are required for each component.

|Role|Requirement|
|--------|---------------|
|Runbook worker|None|
|Automation web service|A certificate that can be used for Secure Sockets Layer \(SSL\) encryption over HTTPS. The installation program for [!INCLUDE[sma_1](../Token/sma_1_md.md)] can be used to generate a self\-signed certificate.|
|Windows PowerShell module|None|

