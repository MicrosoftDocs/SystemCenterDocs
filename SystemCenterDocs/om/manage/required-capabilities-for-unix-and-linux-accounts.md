---
ms.assetid: 97e6a5fa-a108-42d0-93f7-c1ac1884f2ae
title: Required Capabilities for UNIX and Linux Accounts
description: This article describes how to the capabilities for privileged and unprivileged access to Linux and UNIX computer with Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 03/09/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Required capabilities for UNIX and Linux accounts

>Applies To: System Center 2016 - Operations Manager

Access to UNIX and Linux computers in System Center 2016 - Operations Manager uses three Run as profiles. One profile is associated with an unprivileged account while the other two accounts are associated with a privileged account or an unprivileged account that is elevated by using `sudo` or `su`.  
  
In the simplest case, a privileged account has capabilities equivalent to a UNIX and Linux root account, while an unprivileged account has capabilities equivalent to a normal user account. However, with some computer versions of UNIX and Linux, and when you use `sudo` for privilege elevation, you can assign more specific capabilities to accounts. In support of such specific assignments, the following table lists the specific capabilities required by accounts that are assigned to each of the three Run as profiles. These descriptions are somewhat generic because information, such as exact file system paths, can vary among different UNIX and Linux computer versions.  
  
> [!NOTE]  
> The following table describes the required capabilities for accounts to communicate with the Operations Manager agent on a managed UNIX or Linux computer, but the agent itself must always run under the root account on the UNIX or Linux computer.  
  
|UNIX and Linux profile|Required capabilities|  
|--------------------------|-------------------------|  
|Action profile|- To log the UNIX or Linux computer on to the network, authenticated by the Pluggable Authentication Modules (PAM). Must have the ability to run a background shell (not connected to a TTY). Interactive logons are not required.<br> - To read any log file that was specified as unprivileged when a custom log file monitor was created, plus the ability to run **/opt/microsoft/scx/bin/scxlogfilereader**.<br> - To fully run any command shell command that was specified as unprivileged when a command\-line monitor, rule, or task was created.<br>- To run **/usr/bin/vmstat** for the **Run VMStat** task.|  
|Privileged profile|- To log the UNIX or Linux computer on to the network, authenticated by the PAM. Must have the ability to run a background shell (not connected to a TTY). Interactive logons are not required. In the case of an account that is elevated by using `sudo`, this requirement applies to the account before it is elevated. - To fully run any shell command line that was specified as privileged when a command-line monitor, rule, or discovery was created. - To have the following log file monitoring capabilities:<br><br> - To read the log file to be monitored.<br><br>   By default, log files such as Syslog are usually set to be readable only by root, and accounts assigned to this profile must be able to read these files. Instead of giving accounts full root privileges, the log file permissions could be changed to grant read access to a secure group, and accounts made a member of that group. Note that if the log file is periodically rotated, you must ensure that the rotation procedure maintains the group permissions. - To read any log file that was specified as privileged when a custom log file monitor was created. - To run **/opt/microsoft/sc/bin/scxlogfilereader**. - To run tasks, recoveries, and diagnostics. These requirements must be met only if the Operations Manager operator explicitly decides to run them.<br><br> - Many recoveries include stopping and restarting a daemon process. These recoveries require the ability to run the service control interfaces (such as **/et/init.d** for Linux, and **svcadm** for Solaris) in order to stop and restart it. Such service control interfaces typically require the ability to run the **kill** command against the daemon process and to run other basic UNIX and Linux commands. - The requirements for other tasks, recoveries, and diagnostics depend on the details of that particular action.|  
|Agent maintenance profile, and for accounts used to install agents for initial monitoring.|- To log the UNIX or Linux computer on to the network by using Secure Shell (SSH), authenticated by the PAM. Must have the ability to run a background shell (not connected to a TTY). Interactive logons are not required. In the case of an account that is elevated by using `sudo`, this requirement applies to the account before it is elevated. - To run the system package installation program, such as **rpm** on Linux, to install the Operations Manager agent. - To read and write the following directories, and to create them and any subdirectories under them if they do not exist:<br><br> - **/opt** - **/opt/microsoft** - **/opt/microsoft/scx** - **/etc/opt/microsoft/scx** - **/var/opt/microsoft/scx** - **/opt/omi** - **/etc/opt/omi** - **/var/opt/omi** - To run the **kill** command against the running Operations Manager agent processes. - To start the Operations Manager agent. - To add and remove a system daemon, including the Operations Manager agent, by using platform tools to do so. - To run basic UNIX and Linux commands, such as **cat**, **ls**, **pwd**, **cp**, **mv**, **rm**, **gzip** (or equivalent).|  

## Important security considerations

The Operations Manager Linux/UNIX agent uses the standard PAM (Pluggable Authentication Module) mechanism on the Linux or UNIX computer to authenticate the user name and password specified in the Action Profile and Privilege Profile.  Any user name with a password that PAM authenticates can perform monitoring functions, including running command lines and scripts that collect monitoring data.  Such monitoring functions are always performed in the context of that user name (unless sudo elevation is explicitly enabled for that user name), so the Operations Manager agent provides no more capability than if the user name were to login to the Linux/UNIX system.

However, the PAM authentication used by the Operations Manager agent does not require that the user name have an interactive shell associated with it.  If your Linux/UNIX account management practices include removing the interactive shell as a way to pseudo-disable an account, such removal does not prevent the account from being used to connect to the Operations Manager agent and perform monitoring functions.  In these cases, you should use additional PAM configuration to ensure that these pseudo-disabled accounts do not authenticate to the Operations Manager agent.
  
## Next steps

- To understand how to authenticate and monitor your UNIX and Linux computers, review [Credentials You Must Have to Access UNIX and Linux Computers](../plan/planning-security-credentials-for-accessing-unix-and-linux-computers.md)  

- To understand how to elevate an unprivileged account for effective monitoring of UNIX and Linux computers, review [How to Configure sudo Elevation and SSH Keys](How-to-Configure-sudo-Elevation-and-SSH-Keys.md)  

- Review the [Configuring SSL Ciphers](Configuring-SSL-Ciphers.md) if you need to reconfigure Operations Manager to use a different cipher.   
  
