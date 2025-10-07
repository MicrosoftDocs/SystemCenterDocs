---
ms.assetid: e81f5d5c-0780-4a2d-8611-c15b23dc47cf
title: Access UNIX and Linux computers in Operations Manager
description: This article highlights accessing UNIX and Linux computers in Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/26/2025
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Access UNIX and Linux computers in Operations Manager



In System Center - Operations Manager, the management server uses two protocols to communicate with the UNIX or Linux computer:  

-   Secure Shell (SSH)  

    Used for installing, upgrading, and removing agents.  

-   Web services for management (WS-Management)  

    Used for all monitoring operations and include the discovery of agents that were already installed.  

The protocol that is used depends on the action or information that is requested on the management server. All actions, such as agent maintenance, monitors, rules, tasks, and recoveries, are configured to use predefined profiles according to their requirement for an unprivileged or privileged account.  

> [!NOTE]  
> All the credentials referred to in this article pertain to accounts that have been established on the UNIX or Linux computer, not to the Operations Manager accounts that are configured during the installation of Operations Manager. Contact your system administrator for credentials and authentication information.  

For detailed instructions for specifying credentials and configuring accounts, see [Set credentials for accessing UNIX and Linux computers](manage-security-create-crossplat-credentials.md).  

## Authentication on the UNIX or Linux computer

In Operations Manager, the system administrator is no longer required to provide the root password of the UNIX or Linux computer to the management server. Now by elevation, an unprivileged account can assume the identity of a privileged account on the UNIX or Linux computer. The elevation process is performed by the UNIX su (superuser) and sudo programs that use the credentials that the management server supplies. For privileged agent maintenance operations that use SSH (such as discovery, deployment, upgrades, uninstall, and agent recovery), support for su, sudo elevation, and support for SSH key authentication (with or without passphrase) is provided. For privileged WS-Management operations (such as viewing secure log file), support for sudo elevation (without password) is added.  

## Access UNIX and Linux computers topics  

-   [Plan security credentials for accessing UNIX and Linux computers](plan-security-crossplat-credentials.md)

    Provides an overview of using credentials to install and maintain agents on UNIX and Linux computers and how they're configured to use Run As accounts and Run As profiles.  

-   [Set credentials for accessing UNIX and Linux computers](manage-security-create-crossplat-credentials.md)  

    Contains specific procedures for specifying credentials for different wizards in Operations Manager.  

-   [Configure sudo Elevation and SSH Keys](manage-security-create-crossplat-sudo-sshkeys.md)  

    Describes how to configure an unprivileged account to be elevated to have privileged access on a UNIX or Linux computer.  

-   [Required capabilities for UNIX and Linux accounts](manage-security-crossplat-capabilities.md)  

    Describes the permissions on the UNIX or Linux computers that are required to be configured with Run As profiles for use by Operations Manager.  

-   [Administer and configure the UNIX - Linux agent](manage-security-administer-crossplat-agent.md)  

    Describes options to administer and configure the UNIX/Linux agent for System Center - Operations Manager.  

## Next steps

- To configure credentials required to securely manage UNIX and Linux computers with Operations Manager, see [Set credentials for accessing UNIX and Linux computers](manage-security-create-crossplat-credentials.md).
- To configure sudo and SSH keys for an unprivileged account and secure communication with Operations Manager, see [Configure sudo elevation and SSH keys](manage-security-create-crossplat-sudo-sshkeys.md).
