---
title: Orchestrator Integration Toolkit Installation
description: This article explains how to install the Orchestrator Integration Toolkit.
author: rayne-wiselman
manager: carmonm
ms.date: 02/02/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
ms.author: raynew
---

# Installation

This article provides the system requirements and steps to install the Orchestrator Integration Toolkit.  

## System Requirements  
 The installation and use of the Orchestrator Integration Toolkit requires the following hardware and software when installed in a standalone environment.  

|Component|Minimum Requirement|  
|---------------|-------------------------|  
|Processor|2.4 GHz Intel Pentium 4; 2.0 GHz Intel Core 2 Duo or equivalent|  
|Memory|1GB|  
|Hard Disk|60MB|  
|Operating System|Windows Server 2012 (64-bit)<br /><br /> Windows Server 2008 R2 (64-bit)<br /><br /> Windows 8 (32-bit or 64-bit)<br /><br /> Windows 7 (32-bit or 64-bit)|  
|Additional Software|Windows Installer version 3.1<br /><br /> Microsoft .NET Framework 3.5, Service Pack 1<br /><br /> Windows Installer XML Toolset (WiX) version 3.5. For System Center 2012 SP1, OIT supports only version 3.5|  

> [!IMPORTANT]
>  The install for the Orchestrator Integration Toolkit will not fail if Microsoft .NET Framework 3.5, Service Pack 1 is not installed, but different operations in the Command-Line Activity Wizard will fail if it is not present. Ensure that Microsoft .NET Framework 3.5, Service Pack 1 is installed before you install the OIT.  

 The Orchestrator Integration Toolkit can also be installed with the Orchestrator server components. In that case, the system requirements for Orchestrator should be used.  

 When using Visual Studio to create activities using the Orchestrator SDK, note the following requirements:  

-   You must target .NET Framework 3.5  

-   You must be using one of the following Visual Studio versions:  

    -   Visual Studio 2010  

    -   Visual Studio 2008  

## Product Installation  

#### To install the Orchestrator Integration Toolkit  

1.  Download System_Center_2012_R2_Orchestrator_Integration_ToolKit.exe from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=39622), and then run the installer. The welcome page displays.  

2.  Click **Next**. The License Agreement page displays. To continue, you must select the checkbox next to **I accept the terms in the License Agreement**, then click **Next**.  

3.  At the User Information page, enter your name and organization information and click **Next**.  

4.  On the next page, click **Install**. Note the security shield icon on the Install button. This indicates the installation will occur using elevated privileges.  

5.  A User Account Control dialog will appear notifying you of the elevated privileges. Click **Yes** to continue the installation. The installation should take no more than 60 seconds.  

6.  When the installation is complete, click Finish to exit the setup wizard.  

## Results of Installing the Integration Toolkit  
 When you install the Orchestrator Integration Toolkit, there are files created on the computer that are used for creating and using Integration Packs.  

-   Integration Toolkit SDK Library – this assembly and XML file are used for developing custom activities using the Orchestrator SDK. These files are installed by default to “C:\Program Files (x86)\Microsoft System Center <version>\Orchestrator\Integration Toolkit\Lib”.For more information about using the SDK, see the [Orchestrator SDK](https://msdn.microsoft.com/en-us/library/hh855054.aspx).

-   Toolkit Integration Pack for Orchestrator – the System Center Integration Pack for Microsoft .NET Framework Activities is used for running and testing Orchestrator-compatible activity assemblies created using the Command-Line Activity Wizard or via custom code using the Orchestrator SDK. The Integration Pack is installed by default to “C:\Program Files (x86)\Microsoft System Center <version>\Orchestrator\Integration Toolkit\Integration Packs”. For more information about the IP, see Integration Toolkit IP.  

 Integration Toolkit Utilities, Wizards and Binary files – all the files needed to run the Command-Line Activity Wizard, Integration Pack Wizard and all their dependent files are by default installed to “C:\Program Files (x86)\Microsoft System Center <version>\Orchestrator\Integration Toolkit\Bin”. For more information about the wizards, see The Command-Line Activity Wizard and The Integration Pack Wizard.  

## Orchestrator Resources  
 In addition to this online reference provided for System Center Orchestrator, there are a number of resources that can provide additional information on building runbooks, using the Integration Toolkit, and best practices.  

|||  
|-|-|  
|Resource|Location|  
|System Center Home|[https://www.microsoft.com/en-us/cloud-platform/system-center](https://www.microsoft.com/en-us/cloud-platform/system-center)|  
|System Center documentation|[https://docs.microsoft.com/en-us/system-center/](https://docs.microsoft.com/en-us/system-center/)|  
|Orchestrator Team Blog on TechNet|[https://blogs.technet.microsoft.com/orchestrator/](https://blogs.technet.microsoft.com/orchestrator/)|  
|Orchestrator Community Releases on CodePlex|[https://archive.codeplex.com/?p=orchestrator](https://archive.codeplex.com/?p=orchestrator)|  
|Orchestrator Community Forums on TechNet|[https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator](https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator)|
