---
ms.assetid: 685eb5ff-d934-4426-8b3e-dd3e102d1c42
title: Manually Uninstalling Agents from UNIX and Linux Computers
description: This article describes how to manually uninstall the Operations Manager agent from UNIX and Linux computers.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 07/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Manually uninstalling agents from UNIX and Linux computers

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

There are three ways to uninstall the UNIX and Linux management packs and agents.

1.  Delete selected UNIX or Linux system management packs from the Operations Manager Operations Console.

2.  Delete an agent from Operations Manager, and uninstall the agent from the monitored computer. It will be uninstalled first from the UNIX or Linux computer.

3.  Delete the agent from Operations Manager without uninstalling it on the UNIX or Linux host.

Use the following procedures to uninstall agents.

## To delete an agent with the UNIX Linux Agent Uninstall Wizard

1.  For more information, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](manage-upgrade-uninstall-crossplat-agent.md).

After the UNIX or Linux computer has been deleted from the list of monitored computers, you must sign in to the monitored computer and manually uninstall the agent. Use the following procedures to manually uninstall agents from UNIX and Linux computers.

### To uninstall the agent from Red Hat enterprise Linux and SUSE Linux enterprise servers

1.  Sign in as the root user, and uninstall the agent by entering

    `rpm -e scx`

2.  To verify that the package is uninstalled, enter

    `rpm -q scx`

### To uninstall the agent from RPM based Universal Linux servers (Oracle)

1.  Sign in as the root user, and uninstall the agent by entering

    `rpm -e scx`

2.  To verify that the package is uninstalled, enter

    `rpm -q scx`

### To uninstall the agent from DEB based Universal Linux servers (Debian and Ubuntu)

1.  Sign in as the root user, and uninstall the agent by entering

    `dpkg -P scx`

2.  To verify that the package is uninstalled, enter

    `dpkg -l scx`

### To uninstall the agent from Solaris computers

1.  Sign in as the root user, and uninstall the agent by entering

    `pkgrm MSFTscx`

2.  To verify that the package is uninstalled, enter

    `pkginfo -I MSFTscx`

### To uninstall the agent from HP-UX

1.  Sign in as the root user, and uninstall the agent by entering

    `swremove scx`

2.  To verify that the package is uninstalled, enter

    `swlist scx`

### To uninstall the agent from IBM AIX

1.  Sign in as the root user, and uninstall the agent by entering

    `installp -u scx`

2.  To verify that the package is uninstalled, enter

    `lslpp -L scx.rte`

## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](manage-install-crossplat-agent-cmdline.md).

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](~/scom/manage-apply-overrides-object-discovery.md).

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](manage-upgrade-uninstall-crossplat-agent.md).
