---
ms.assetid: 97e6a5fa-a108-42d0-93f7-c1ac1884f2ae
title: Required Capabilities for UNIX and Linux Accounts
description: This article describes the capabilities for privileged and unprivileged access to Linux and UNIX computer with Operations Manager
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/07/2025
ms.custom: UpdateFrequency3
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Required capabilities for UNIX and Linux accounts



Access to UNIX and Linux computers in System Center - Operations Manager uses three Run as profiles. One profile is associated with an unprivileged account while the other two accounts are associated with a privileged account or an unprivileged account that is elevated by using `sudo` or `su`.  

In the simplest case, a privileged account has capabilities equivalent to a UNIX and Linux root account, while an unprivileged account has capabilities equivalent to a normal user account. However, with some computer versions of UNIX and Linux, and when you use `sudo` for privilege elevation, you can assign more specific capabilities to accounts.

The following table lists the specific capabilities required by accounts that are assigned to each of the three Run as profiles. These descriptions are generic because, information such as exact file system paths, can vary among different UNIX and Linux computer versions.  

> [!NOTE]  
> The following table describes the required capabilities for accounts to communicate with the Operations Manager agent on a managed UNIX or Linux computer, but the agent itself must always run under the root account on the UNIX or Linux computer.  

|UNIX and Linux profile|Required capabilities|  
|--------------------------|-------------------------|  
|Action profile|To log the UNIX or Linux computer on to the network, authenticated by the Pluggable Authentication Modules (PAM). Must have the ability to run a background shell (not connected to a TTY). Interactive logons aren't required.<br> To read any log file that was specified as unprivileged when a custom log file monitor was created, plus the ability to run **/opt/microsoft/scx/bin/scxlogfilereader**.<br> To fully run any command shell command that was specified as unprivileged, when a command\-line monitor, rule, or task was created.<br>To run **/usr/bin/vmstat** for the **Run VMStat** task.|  
|Privileged profile|Log the UNIX or Linux computer on to the network, authenticated by the PAM. Must have the ability to run a background shell (not connected to a TTY). Interactive logons aren't required. In the case of an account that is elevated by using `sudo`, this requirement applies to the account before it's elevated.<br> Fully run any shell command line that was specified as privileged, when a command-line monitor, rule, or discovery was created.<br> Have the following log file monitoring capabilities:<br><br> - Read the log file to be monitored.<br>  By default, log files such as Syslog are  set to be readable only by root, and accounts assigned to this profile can read these files. Instead of giving accounts full root privileges, you can change the log file permissions to grant read access to a secure group, and accounts made a member of that group. If the log file is periodically rotated, you must ensure the rotation procedure maintains the group permissions. - To read any log file that was specified as privileged when a custom log file monitor was created. - To run **/opt/microsoft/sc/bin/scxlogfilereader**. - Run tasks, recoveries, and diagnostics. These requirements must be met only if the Operations Manager operator explicitly decides to run them.<br><br> - Many recoveries include stopping and restarting a daemon process. These recoveries require the ability to run the service control interfaces such as **/et/init.d** for Linux, and **svcadm** for Solaris to stop and restart it. Such service control interfaces typically require the ability to run the **kill** command against the daemon process and to run other basic UNIX and Linux commands. - The requirements for other tasks, recoveries, and diagnostics depend on the details of that particular action.|  
|Agent maintenance profile, and for accounts used to install agents for initial monitoring|Log the UNIX or Linux computer on to the network by using Secure Shell (SSH), authenticated by the PAM. Must have the ability to run a background shell (not connected to a TTY). Interactive logons aren't required. In the case of an account that is elevated by using `sudo`, this requirement applies to the account before it's elevated.<br> Run the system package installation program, such as **rpm** on Linux, to install the Operations Manager agent.<br> Read and write the following directories, and to create them and any subdirectories under them if they don't exist:<br><br> - **/opt** - **/opt/microsoft** - **/opt/microsoft/scx** - **/etc/opt/microsoft/scx** - **/var/opt/microsoft/scx** - **/opt/omi** - **/etc/opt/omi** - **/var/opt/omi**</ul>Run the **kill** command against the running Operations Manager agent processes.<br> Start the Operations Manager agent.<br> Add and remove a system daemon, including the Operations Manager agent, by using platform tools to do so.<br> Run basic UNIX and Linux commands, such as **cat**, **ls**, **pwd**, **cp**, **mv**, **rm**, **gzip** (or equivalent).|  

## Important security considerations

The Operations Manager Linux/UNIX agent uses the standard PAM (Pluggable Authentication Module) mechanism on the Linux or UNIX computer to authenticate the user name and password that is specified in the Action Profile and Privilege Profile.  Any user name with a password that PAM authenticates can perform monitoring functions, including running command lines and scripts that collect monitoring data. Such monitoring functions are always performed in the context of that user name, unless sudo elevation is explicitly enabled for that user name. So, the Operations Manager agent provides no more capability than if the user name were to sign in to the Linux/UNIX system.

However, the PAM authentication that is used by the Operations Manager agent doesn't require that the user name have an interactive shell associated with it.  If your Linux/UNIX account management practices include removing the interactive shell as a way to pseudo-disable an account, such removal doesn't prevent the account from being used to connect to the Operations Manager agent and perform monitoring functions.  In these cases, use additional PAM configuration to ensure these pseudo-disabled accounts don't authenticate to the Operations Manager agent.

## Next steps

- To understand how to authenticate and monitor your UNIX and Linux computers, review [Credentials you must have to access UNIX and Linux computers](plan-security-crossplat-credentials.md).
- To understand how to elevate an unprivileged account for effective monitoring of UNIX and Linux computers, review [How to configure sudo elevation and SSH keys](manage-security-create-crossplat-sudo-sshkeys.md).
- If you need to reconfigure Operations Manager to use a different cipher, review the [Configure SSL ciphers](manage-security-crossplat-config-sslcipher.md).
