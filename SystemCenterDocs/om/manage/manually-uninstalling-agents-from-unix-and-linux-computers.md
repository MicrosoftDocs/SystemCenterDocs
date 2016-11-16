---
ms.assetid: 685eb5ff-d934-4426-8b3e-dd3e102d1c42
title:  Manually Uninstalling Agents from UNIX and Linux Computers
description: This article describes how to manually uninstall the Operations Manager agent from UNIX and Linux computers.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Manually uninstalling agents from UNIX and Linux computers

>Applies To: System Center 2016 - Operations Manager

There are three ways to uninstall the UNIX and Linux management packs and agents.

1.  Delete selected UNIX or Linux system management packs from the Operations Manager Operations Console.

2.  Delete an agent from Operations Manager, and uninstall the agent from the monitored computer. It will be uninstalled first from the UNIX or Linux computer.

3.  Delete the agent from Operations Manager without uninstalling it on the UNIX or Linux host.

Use the following procedures to uninstall agents.

## To delete an agent with the UNIX Linux Agent Uninstall Wizard

1.  For more information, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md).

After the UNIX or Linux computer has been deleted from the list of monitored computers, you must log on to the monitored computer and manually uninstall the agent. Use the following procedures to manually uninstall agents from UNIX and Linux computers.

### To uninstall the agent from Red Hat enterprise Linux and SUSE Linux enterprise servers

1.  Log on as the root user, and uninstall the agent by typing

    **rpm -e scx**

2.  To verify that the package is uninstalled, type

    **rpm -q scx**

### To uninstall the agent from RPM based Universal Linux servers (Oracle and Centos)

1.  Log on as the root user, and uninstall the agent by typing

    **rpm -e scx**

2.  To verify that the package is uninstalled, type

    **rpm -q scx**

### To uninstall the agent from DEB based Universal Linux servers (Debian and Ubuntu)

1.  Log on as the root user, and uninstall the agent by typing

    **dpkg -P scx**

2.  To verify that the package is uninstalled, type

    **dpkg -l scx**

### To uninstall the agent from Solaris computers

1.  Log on as the root user, and uninstall the agent by typing

    **pkgrm MSFTscx**

2.  To verify that the package is uninstalled, type

    **pkginfo -I MSFTscx**

### To uninstall the agent from HP-UX

1.  Log on as the root user, and uninstall the agent by typing

    **swremove scx**

2.  To verify that the package is uninstalled, type

    **swlist scx**

### To uninstall the agent from IBM AIX

1.  Log on as the root user, and uninstall the agent by typing

    **installp -u scx**

2.  To verify that the package is uninstalled, type

    **lslpp -L scx.rte**

## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md).

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md).

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md).


