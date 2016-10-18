---
ms.assetid: e81f5d5c-0780-4a2d-8611-c15b23dc47cf
title: Accessing UNIX and Linux Computers in Operations Manager
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 10/12/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Accessing UNIX and Linux Computers in Operations Manager

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, the management server uses two protocols to communicate with the UNIX or Linux computer:  
  
-   Secure Shell (SSH)  
  
    Used for installing, upgrading, and removing agents.  
  
-   Web Services for Management (WS-Management)  
  
    Used for all monitoring operations and include the discovery of agents that were already installed.  
  
The protocol that is used depends on the action or information that is requested on the management server. All actions, such as agent maintenance, monitors, rules, tasks, and recoveries, are configured to use predefined profiles according to their requirement for an unprivileged or privileged account.  
  
> [!NOTE]  
> All credentials referred to in this topic pertain to accounts that have been established on the UNIX or Linux computer, not to the Operations Manager accounts that are configured during the installation of Operations Manager. Contact your system administrator for credentials and authentication information.  
  
For detailed instructions for specifying credentials and configuring accounts, see [How to Set Credentials for Accessing UNIX and Linux Computers](How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md).  
  
## Authentication on the UNIX or Linux Computer  
In Operations Manager, the system administrator is no longer is required to provide the root password of the UNIX or Linux computer to the management server. Now by elevation, an unprivileged account can assume the identity of a privileged account on the UNIX or Linux computer. The elevation process is performed by the UNIX su (superuser) and sudo programs that use the credentials that the management server supplies. For privileged agent maintenance operations that use SSH (such as discovery, deployment, upgrades, uninstall, and agent recovery), support for su, sudo elevation, and support for SSH key authentication (with or without passphrase) is provided. For privileged WS-Management operations (such as viewing secure log file), support for sudo elevation (without password) is added.  
  
## Accessing UNIX and Linux Computers Topics  
  
-   [Planning Security Credentials for Accessing UNIX and Linux Computers](../plan/planning-security-credentials-for-accessing-unix-and-linux-computers.md) 
  
    Provides an overview of using credentials to install and maintain agents on UNIX and Linux computers and how they are configured to use Run As accounts and Run As profiles.  
  
-   [How to Set Credentials for Accessing UNIX and Linux Computers](How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md)  
  
    Contains specific procedures for specifying credentials for different wizards in Operations Manager.  
  
-   [How to Configure sudo Elevation and SSH Keys](How-to-Configure-sudo-Elevation-and-SSH-Keys.md)  
  
    Describes how to configure an unprivileged account to be elevated to have privileged access on a UNIX or Linux computer.  
  
-   [Required Capabilities for UNIX and Linux Accounts](Required-Capabilities-for-UNIX-and-Linux-Accounts.md)  
  
    Describes the permissions on the UNIX or Linux computers that are required to be configured with Run As profiles for use by Operations Manager.  
  
-   [Administering and Configuring the UNIX - Linux Agent](Administering-and-Configuring-the-UNIX-Linux-Agent.md)  
  
    Describes options to administer and configure the UNIX/Linux agent for System Center 2016 - Operations Manager.  
  

