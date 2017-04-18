---
ms.assetid: 5556c9cf-088c-422a-9a21-0612fb674e7c
title:  Managing Discovery and Agents
description: This article highlights the section titles contained within this section of the Operations Manager 2016 documentation. 
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Managing discovery and agents

>Applies To: System Center 2016 - Operations Manager

System Center Operations Manager can monitor computers running Windows, UNIX, and Linux operating systems. For a list of the supported operating system versions, see [Supported Configurations](../../scom/plan-system-requirements.md).

To begin monitoring, computers must be discovered. For a description of the discovery process, see "How Objects Are Discovered and Monitored" in [Key Concepts](../get-started/Operations-Manager-Key-Concepts.md).

Comprehensive monitoring requires that an agent be installed on the discovered computer. This section explains how to discover computers, install agents on discovered computers, and configure agents. It also provides instructions for uninstalling agents. For information about monitoring computers without installing an agent, see [Agentless Monitoring in Operations Manager](https://technet.microsoft.com/library/hh212910%28v=sc.12%29.aspx) and [Client Monitoring Using Agentless Exception Monitoring in Operations Manager](https://technet.microsoft.com/library/hh230748%28v=sc.12%29.aspx).

> [!NOTE]
> For problems with discovery, see [Troubleshooting Discovery in Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=235123).

## Managing discovery and agents topics

-   [Discover and install agent on Windows](install-agent-on-windows-using-the-discovery-wizard.md)

    This section provides the information you need for discovering and installing the Windows agents to be monitored by Operations Manager.

-   [Discover and install agent on UNIX and Linux](install-agent-on-unix-and-linux-using-the-discovery-wizard.md)

    This section provides the information you need for discovering and installing the UNIX and Linux agents to be monitored by Operations Manager.

-   [Install Windows agent manually with MOMAgent.msi](install-windows-agent-manually-using-momagent.md)

     This section provides the information you need for manually installing the Windows agent and approve them to be monitored by Operations Manager using the MOMAgent.msi Windows Installer package.

-   [Install agent on Nano Server](install-agent-on-nano-server.md)

    This section provides the information you need for installing the Nano Server agent to be monitored by Operations Manager.

-   [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)

    This section provides the information you need for manually installing the UNIX and Linux agent and configuring the self-signed certificates required to be monitored by Operations Manager.

-   [Process manual agent installations](process-manual-agent-installations.md)

    This section describes how to configure settings for manual agent installations in your Operations Manager management group.

-   [Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)

    This section provides the information you need to understand how to limit or restrict discovery for monitored objects in your management group.

-   [Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)

    This section describes how to upgrade and uninstall agents on UNIX and Linux computers either from the Operations console.  

-   [Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)

    This section describes the ways to uninstall the UNIX and Linux management packs and agents from UNIX and Linux computers.

-   [Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md)

    This section describes the ways to uninstall the Windows agent from Windows computers.




