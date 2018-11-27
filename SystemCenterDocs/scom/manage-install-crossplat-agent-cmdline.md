---
ms.assetid: 
title: Install agent on UNIX and Linux computers from the command line
description: Article to detail how to install the System Center Operations Manager agent manually on UNIX and Linux computers.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 08/14/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# Install agent on UNIX and Linux computers from the command line

::: moniker range=">=sc-om-1801"

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center Operations Manager version 1801 and higher.  The agent packages can be found in the following folder on a management server - *%ProgramFiles%\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits*.  Import the required management packs for the specific version of UNIX/Linux you need to monitor.  The management packs are available in the Operations Manager installation media, in the *\ManagementPacks* directory or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=29696).

::: moniker-end

::: moniker range="sc-om-2016"

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center 2016 - Operations Manager.  The agent packages can be found in the following folder on a management server - *%ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits*.  Import the required management packs for the specific version of UNIX/Linux you need to monitor.  The management packs are available in the Operations Manager installation media, in the *\ManagementPacks* directory or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=29696).

::: moniker-end

::: moniker range=">=sc-om-1801"

[!INCLUDE [install-om-crossplat-agent-cmdline-1801.md](../includes/install-om-crossplat-agent-cmdline-1801.md)]

::: moniker-end

::: moniker range="sc-om-2016"

[!INCLUDE [install-om-crossplat-agent-cmdline-2016](../includes/install-om-crossplat-agent-cmdline-2016.md)]

::: moniker-end

## Next steps

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](~/scom/manage-apply-overrides-object-discovery.md)

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md)

- Review [Manually Uninstalling Agents from UNIX and Linux Computers](~/scom/manage-uninstall-crossplat-agent.md) to understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers.  
