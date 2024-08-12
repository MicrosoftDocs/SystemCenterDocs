---
title: Orchestrator Integration Toolkit Installation
description: This article explains how to install the Orchestrator Integration Toolkit.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 08/09/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
ms.custom: intro-installation
---

# Installation

> [!CAUTION]
> This article references Windows Server 2012 and 2012 R2 reached End Of Support. Consider your use and planning accordingly. For more information, see the [Windows Server 2012 and 2012 R2 End of Support guidance](/lifecycle/products/windows-server-2012-r2).

This article provides the system requirements and steps to install the Orchestrator Integration Toolkit.  

## System Requirements

 The installation and use of the Orchestrator Integration Toolkit requires the following hardware and software when installed in a standalone environment.  

::: moniker range="<=sc-orch-2019"

|Component|Minimum Requirement|  
|---------------|-------------------------|  
|Processor|2.4 GHz Intel Pentium 4; 2.0 GHz Intel Core 2 Duo or equivalent|  
|Memory|1 GB|  
|Hard Disk|60 MB|  
|Operating System|Windows Server 2012 (64-bit)<br /><br /> Windows Server 2008 R2 (64-bit)<br /><br /> Windows 8 (32-bit or 64-bit)<br /><br /> Windows 7 (32-bit or 64-bit)|  
|Additional Software|Windows Installer version 3.1<br /><br /> Microsoft .NET Framework 3.5, Service Pack 1<br /><br /> Windows Installer XML Toolset (WiX) version 3.5. For System Center 2012 SP1, OIT supports only version 3.5|  

::: moniker-end

::: moniker range=">=sc-orch-2022"

|Component|Minimum Requirement|  
|---------------|-------------------------|  
|Processor|2.4 GHz Intel Pentium 4; 2.0 GHz Intel Core 2 Duo or equivalent|  
|Memory|Minimum 1 GB (recommended 2 GB)|  
|Hard Disk|200 MB|  
|Operating System|Windows Server 2012 or later|  
|Additional Software|Windows Installer XML Toolset (WiX) version 3.11. For System Center 2012 SP1, OIT supports only version 3.5|  

::: moniker-end

> [!IMPORTANT]
> The install for the Orchestrator Integration Toolkit won't fail if Microsoft .NET Framework 3.5, Service Pack 1 is not installed, but different operations in the Command-Line Activity Wizard will fail if it isn't present. Ensure that Microsoft .NET Framework 3.5, Service Pack 1 is installed before you install the OIT.  

 The Orchestrator Integration Toolkit can also be installed with the Orchestrator server components. In that case, the system requirements for Orchestrator should be used.  

 When using Visual Studio to create activities using the Orchestrator SDK, you must target .NET Framework 4.0 or higher (we recommend .NET Framework v4.7.2).

## Product Installation  

#### Install the Orchestrator Integration Toolkit

::: moniker range="<=sc-orch-2019"

1. Download `System_Center_2012_R2_Orchestrator_Integration_ToolKit.exe` from the [Microsoft download center](https://www.microsoft.com/download), and run the installer. The welcome page appears.  

::: moniker-end

::: moniker range=">=sc-orch-2022"

1. Download `System_Center_Orchestrator_IntegrationToolKit-10.22.*.*.exe` from [Microsoft Download center](https://www.microsoft.com/download/details.aspx?id=104133) and run the installer. The welcome page appears.

::: moniker-end

2. Select **Next**. The License Agreement page displays. To continue, you must select the checkbox next to **I accept the terms in the License Agreement** and select **Next**.  

3. At the User Information page, enter your name and organization information and select **Next**.  

4. On the next page, select **Install**. Note the security shield icon on the Install button. This indicates the installation will occur using elevated privileges.  

5. A User Account Control dialog will appear notifying you of the elevated privileges. Select **Yes** to continue the installation. The installation should take no more than 60 seconds.  

6. When the installation is complete, select **Finish** to exit the setup wizard.  

## Results of Installing the Integration Toolkit

 When you install the Orchestrator Integration Toolkit, there are files created on the computer that are used for creating and using Integration Packs.  

::: moniker range="<=sc-orch-2019"

- Integration Toolkit SDK Library – This assembly and XML file are used for developing custom activities using the Orchestrator SDK. These files are installed by default to `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Integration Toolkit\Lib`. For more information about using the SDK, see the [Orchestrator SDK](/previous-versions/system-center/developer/hh855054(v=msdn.10)).

- Toolkit Integration Pack for Orchestrator – The System Center Integration Pack for Microsoft .NET Framework Activities is used for running and testing Orchestrator-compatible activity assemblies created using the Command-Line Activity Wizard or via custom code using the Orchestrator SDK. The Integration Pack is installed by default to `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Integration Toolkit\Integration Packs`.

  **Integration Toolkit Utilities, Wizards, and Binary files** – All the files needed to run the Command-Line Activity Wizard, Integration Pack Wizard, and all their dependent files are by default installed to `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Integration Toolkit\Bin`. For more information about the wizards, see [The Command-Line Activity Wizard][cli-wizard] and [The Integration Pack Wizard][ip-wizard].  

::: moniker-end

::: moniker range=">=sc-orch-2022"

- Integration Toolkit SDK Library – This assembly and XML file are used for developing custom activities using the Orchestrator SDK. These files are installed by default to `C:\Program Files\Microsoft System Center\Orchestrator\Integration Toolkit\Lib`. For more information about using the SDK, see the [Orchestrator SDK](/previous-versions/system-center/developer/hh855054(v=msdn.10)).

- Toolkit Integration Pack for Orchestrator – The System Center Integration Pack for Microsoft .NET Framework Activities is used for running and testing Orchestrator-compatible activity assemblies created using the Command-Line Activity Wizard or via custom code using the Orchestrator SDK. The Integration Pack is installed by default to `C:\Program Files\Microsoft System Center\Orchestrator\Integration Toolkit\Integration Packs`.

  Integration Toolkit Utilities, Wizards, and Binary files – All the files needed to run the Command-Line Activity Wizard, Integration Pack Wizard, and all their dependent files are by default installed to `C:\Program Files\Microsoft System Center\Orchestrator\Integration Toolkit\Bin`. For more information about the wizards, see [The Command-Line Activity Wizard][cli-wizard] and [The Integration Pack Wizard][ip-wizard].

::: moniker-end

[cli-wizard]: ./command-line-activity-wizard.md
[ip-wizard]: ./integration-pack-wizard.md

## Orchestrator Resources

In addition to this online reference provided for System Center Orchestrator, there are many resources that can provide additional information on building runbooks, using the Integration Toolkit, and best practices.

- [System Center home](https://www.microsoft.com/cloud-platform/system-center)
- [System Center documentation](../index.yml)
- [Orchestrator team blog](https://blogs.technet.microsoft.com/orchestrator/)
- [Orchestrator community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator)|
