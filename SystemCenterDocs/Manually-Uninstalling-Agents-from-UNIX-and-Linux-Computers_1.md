---
title: Manually Uninstalling Agents from UNIX and Linux Computers_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a55e655-b615-4921-a96d-f62877c8db12
---
# Manually Uninstalling Agents from UNIX and Linux Computers_1
There are three ways to uninstall the UNIX and Linux management packs and agents.

1.  Delete selected UNIX or Linux system management packs from the Operations Manager Operations Console.

2.  Delete an agent from Operations Manager, and uninstall the agent from the monitored computer. It will be uninstalled first from the UNIX or Linux computer.

3.  Delete the agent from Operations Manager without uninstalling it on the UNIX or Linux host.

Use the following procedures to uninstall agents.

### To delete an agent with the UNIX Linux Agent Uninstall Wizard

1.  For more information, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](./Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md).

After the UNIX or Linux computer has been deleted from the list of monitored computers, you must log on to the monitored computer and manually uninstall the agent. Use the following procedures to manually uninstall agents from UNIX and Linux computers.

### To uninstall the agent from Red Hat enterprise Linux and SUSE Linux enterprise servers

1.  Log on as the root user, and uninstall the agent by typing

    **rpm –e scx**

2.  To verify that the package is uninstalled, type

    **rpm –q scx**

### To uninstall the agent from RPM based Universal Linux servers \(Oracle and Centos\)

1.  Log on as the root user, and uninstall the agent by typing

    **rpm –e scx**

2.  To verify that the package is uninstalled, type

    **rpm –q scx**

### To uninstall the agent from DEB based Universal Linux servers \(Debian and Ubuntu\)

1.  Log on as the root user, and uninstall the agent by typing

    **dpkg –P scx**

2.  To verify that the package is uninstalled, type

    **dpkg –l scx**

### To uninstall the agent from Solaris computers

1.  Log on as the root user, and uninstall the agent by typing

    **pkgrm MSFTscx**

2.  To verify that the package is uninstalled, type

    **pkginfo –I MSFTscx**

### To uninstall the agent from HP\-UX

1.  Log on as the root user, and uninstall the agent by typing

    **swremove scx**

2.  To verify that the package is uninstalled, type

    **swlist scx**

### To uninstall the agent from IBM AIX

1.  Log on as the root user, and uninstall the agent by typing

    **installp –u scx**

2.  To verify that the package is uninstalled, type

    **lslpp –L scx.rte**

## See Also
[Operations Manager Agent Installation Methods](./Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](./Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](./Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](./Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](./Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Managing Certificates for UNIX and Linux Computers](./Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Process Manual Agent Installations](./Process-Manual-Agent-Installations.md)
[Applying Overrides to Object Discoveries](./Applying-Overrides-to-Object-Discoveries.md)
[Configuring Agents](./Configuring-Agents.md)
[Examples of Using MOMAgent Command to Manage Agents](./Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](./Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Install Agent Using the Command Line](./Install-Agent-Using-the-Command-Line.md)
[Uninstall Agent from Windows-based Computers](./Uninstall-Agent-from-Windows-based-Computers.md)


