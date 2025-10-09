---
title: Install agent on UNIX and Linux computers from the command line
description: Article to detail how to install the System Center Operations Manager agent manually on UNIX and Linux computers.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/01/2025
ms.custom: UpdateFrequency2, intro-installation, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install agent on UNIX and Linux computers from the command line

::: moniker range="sc-om-2025"

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center Operations Manager version 2025. The agent packages can be found in the following folder on a management server - `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits`. Import the required management packs for the specific version of UNIX/Linux you need to monitor. The management packs are available in the Operations Manager installation media, in the `\ManagementPacks` folder or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=106248).

::: moniker-end

::: moniker range="sc-om-2019"

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center Operations Manager version 2019. The agent packages can be found in the following folder on a management server - `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits`. Import the required management packs for the specific version of UNIX/Linux you need to monitor. The management packs are available in the Operations Manager installation media in the `\ManagementPacks` folder, or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=58208).

::: moniker-end

::: moniker range="sc-om-2022"

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center Operations Manager version 2022. The agent packages can be found in the following folder on a management server - `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits`. Import the required management packs for the specific version of UNIX/Linux you need to monitor. The management packs are available in the Operations Manager installation media, in the `\ManagementPacks` folder or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=104213).

::: moniker-end

::: moniker range="sc-om-2016"

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center 2016 - Operations Manager.  The agent packages can be found in the following folder on a management server - `%ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits`. Import the required management packs for the specific version of UNIX/Linux you need to monitor. The management packs are available in the Operations Manager installation media, in the `\ManagementPacks` folder or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=58208).

::: moniker-end

::: moniker range="sc-om-2025"

[!INCLUDE [install-om-crossplat-agent-cmdline-2025](../includes/install-om-crossplat-agent-cmdline-2025.md)]

::: moniker-end

::: moniker range="sc-om-2022"

[!INCLUDE [install-om-crossplat-agent-cmdline-2022](../includes/install-om-crossplat-agent-cmdline-2022.md)]

::: moniker-end

::: moniker range="sc-om-2019"

[!INCLUDE [install-om-crossplat-agent-cmdline-2019](../includes/install-om-crossplat-agent-cmdline-2019.md)]

::: moniker-end



::: moniker range="sc-om-2016"

[!INCLUDE [install-om-crossplat-agent-cmdline-2016](../includes/install-om-crossplat-agent-cmdline-2016.md)]

::: moniker-end

## Next steps

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](~/scom/manage-apply-overrides-object-discovery.md).

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md).

- To understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers, review [Manually Uninstalling Agents from UNIX and Linux Computers](~/scom/manage-uninstall-crossplat-agent.md).  
