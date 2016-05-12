---
title: Accessing UNIX and Linux Computers in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c09d5b3b-a76d-412a-bb4d-32d6f1d3047a
---
# Accessing UNIX and Linux Computers in Operations Manager
In [!INCLUDE[om12long](Token/om12long_md.md)], the management server uses two protocols to communicate with the UNIX or Linux computer:

-   Secure Shell \(SSH\)

    Used for installing, upgrading, and removing agents.

-   Web Services for Management \(WS\-Management\)

    Used for all monitoring operations and include the discovery of agents that were already installed.

The protocol that is used depends on the action or information that is requested on the management server. All actions, such as agent maintenance, monitors, rules, tasks, and recoveries, are configured to use predefined profiles according to their requirement for an unprivileged or privileged account.

> [!NOTE]
> All credentials referred to in this topic pertain to accounts that have been established on the UNIX or Linux computer, not to the [!INCLUDE[om12short](Token/om12short_md.md)] accounts that are configured during the installation of [!INCLUDE[om12short](Token/om12short_md.md)]. Contact your system administrator for credentials and authentication information.

For detailed instructions for specifying credentials and configuring accounts, see [How to Set Credentials for Accessing UNIX and Linux Computers](How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md).

## Authentication on the UNIX or Linux Computer
In [!INCLUDE[om12short](Token/om12short_md.md)], the system administrator is no longer is required to provide the root password of the UNIX or Linux computer to the management server. Now by elevation, an unprivileged account can assume the identity of a privileged account on the UNIX or Linux computer. The elevation process is performed by the UNIX su \(superuser\) and sudo programs that use the credentials that the management server supplies. For privileged agent maintenance operations that use SSH \(such as discovery, deployment, upgrades, uninstallation, and agent recovery\), support for su, sudo elevation, and support for SSH key authentication \(with or without passphrase\) is provided. For privileged WS\-Management operations \(such as viewing secure log files\), support for sudo elevation \(without password\) is added.

## Accessing UNIX and Linux Computers Topics

-   [Credentials You Must Have to Access UNIX and Linux Computers](Credentials-You-Must-Have-to-Access-UNIX-and-Linux-Computers.md)

    Provides an overview of using credentials to install and maintain agents on UNIX and Linux computers and how they are configured to use Run As accounts and Run As profiles.

-   [How to Set Credentials for Accessing UNIX and Linux Computers](How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md)

    Contains specific procedures for specifying credentials for different wizards in [!INCLUDE[om12short](Token/om12short_md.md)].

-   [How to Configure sudo Elevation and SSH Keys](How-to-Configure-sudo-Elevation-and-SSH-Keys.md)

    Describes how to configure an unprivileged account to be elevated to have privileged access on a UNIX or Linux computer.

-   [Required Capabilities for UNIX and Linux Accounts](Required-Capabilities-for-UNIX-and-Linux-Accounts.md)

    Describes the permissions on the UNIX or Linux computers that are required to be configured with Run As profiles for use by [!INCLUDE[om12short](Token/om12short_md.md)].

-   [Administering and Configuring the UNIX - Linux Agent](Administering-and-Configuring-the-UNIX---Linux-Agent.md)

    Describes options to administer and configure the UNIX\/Linux agent for System Center – [!INCLUDE[omblue_2](Token/omblue_2_md.md)].

## Other Resources for this Feature

-   [Managing Access in Operations Manager](Managing-Access-in-Operations-Manager.md)

-   [Credentials You Must Have to Access UNIX and Linux Computers](Credentials-You-Must-Have-to-Access-UNIX-and-Linux-Computers.md)

-   [Implementing User Roles](Implementing-User-Roles.md)

-   [How to Create a New Action Account in Operations Manager](How-to-Create-a-New-Action-Account-in-Operations-Manager.md)

-   [How to Manage the Report Server Unattended Execution Account in Operations Manager](How-to-Manage-the-Report-Server-Unattended-Execution-Account-in-Operations-Manager.md)

-   [Control Access by Using the Health Service Lockdown Tool in Operations Manager](Control-Access-by-Using-the-Health-Service-Lockdown-Tool-in-Operations-Manager.md)

-   [Managing Run As Accounts and Profiles](Managing-Run-As-Accounts-and-Profiles.md)


