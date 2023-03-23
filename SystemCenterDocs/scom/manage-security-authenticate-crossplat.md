---
ms.assetid: e81f5d5c-0780-4a2d-8611-c15b23dc47cf
title: Accessing UNIX and Linux Computers in Operations Manager
description: This article highlights accessing UNIX and Linux computers in Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 04/29/2019
ms.custom: UpdateFrequency2
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Accessing UNIX and Linux computers in Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

In System Center - Operations Manager, the management server uses two protocols to communicate with the UNIX or Linux computer:  

-   Secure Shell (SSH)  

    Used for installing, upgrading, and removing agents.  

-   Web Services for Management (WS-Management)  

    Used for all monitoring operations and include the discovery of agents that were already installed.  

The protocol that is used depends on the action or information that is requested on the management server. All actions, such as agent maintenance, monitors, rules, tasks, and recoveries, are configured to use predefined profiles according to their requirement for an unprivileged or privileged account.  

> [!NOTE]  
> All the credentials referred to in this article pertain to accounts that have been established on the UNIX or Linux computer, not to the Operations Manager accounts that are configured during the installation of Operations Manager. Contact your system administrator for credentials and authentication information.  

For detailed instructions for specifying credentials and configuring accounts, see [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).  

## Authentication on the UNIX or Linux computer

In Operations Manager, the system administrator is no longer required to provide the root password of the UNIX or Linux computer to the management server. Now by elevation, an unprivileged account can assume the identity of a privileged account on the UNIX or Linux computer. The elevation process is performed by the UNIX su (superuser) and sudo programs that use the credentials that the management server supplies. For privileged agent maintenance operations that use SSH (such as discovery, deployment, upgrades, uninstall, and agent recovery), support for su, sudo elevation, and support for SSH key authentication (with or without passphrase) is provided. For privileged WS-Management operations (such as viewing secure log file), support for sudo elevation (without password) is added.  

## Accessing UNIX and Linux computers topics  

-   [Planning Security Credentials for Accessing UNIX and Linux Computers](plan-security-crossplat-credentials.md)

    Provides an overview of using credentials to install and maintain agents on UNIX and Linux computers and how they're configured to use Run As accounts and Run As profiles.  

-   [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md)  

    Contains specific procedures for specifying credentials for different wizards in Operations Manager.  

-   [How to Configure sudo Elevation and SSH Keys](manage-security-create-crossplat-sudo-sshkeys.md)  

    Describes how to configure an unprivileged account to be elevated to have privileged access on a UNIX or Linux computer.  

-   [Required Capabilities for UNIX and Linux Accounts](manage-security-crossplat-capabilities.md)  

    Describes the permissions on the UNIX or Linux computers that are required to be configured with Run As profiles for use by Operations Manager.  

-   [Administering and Configuring the UNIX - Linux Agent](manage-security-administer-crossplat-agent.md)  

    Describes options to administer and configure the UNIX/Linux agent for System Center 2016 - Operations Manager.  
