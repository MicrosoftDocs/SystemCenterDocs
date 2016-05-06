---
title: Required Capabilities for UNIX and Linux Accounts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ced31d23-9631-42a7-b367-9c71f9dd0bdf
---
# Required Capabilities for UNIX and Linux Accounts
Access to UNIX and Linux computers in [!INCLUDE[om12long](./Token/om12long_md.md)] uses three Run as profiles. One profile is associated with an unprivileged account while the other two accounts are associated with a privileged account or an unprivileged account that is elevated by using `sudo` or `su`.

In the simplest case, a privileged account has capabilities equivalent to a UNIX and Linux root account, while an unprivileged account has capabilities equivalent to a normal user account. However, with some computer versions of UNIX and Linux, and when you use `sudo` for privilege elevation, you can assign more specific capabilities to accounts. In support of such specific assignments, the following table lists the specific capabilities required by accounts that are assigned to each of the three Run as profiles. These descriptions are somewhat generic because information, such as exact file system paths, can vary among different UNIX and Linux computer versions.

> [!NOTE]
> The following table describes the required capabilities for accounts to communicate with the [!INCLUDE[om12short](./Token/om12short_md.md)] agent on a managed UNIX or Linux computer, but the agent itself must always run under the root account on the UNIX or Linux computer.

|UNIX and Linux profile|Required capabilities|
|--------------------------|-------------------------|
|Action profile|-   To log the UNIX or Linux computer on to the network, authenticated by the Pluggable Authentication Modules \(PAM\). Must have the ability to run a background shell \(not connected to a TTY\). Interactive logons are not required.<br />-   To read any log file that was specified as unprivileged when a custom log file monitor was created, plus the ability to run **\/opt\/microsoft\/scx\/bin\/scxlogfilereader**.<br />-   To fully run any command shell command that was specified as unprivileged when a command\-line monitor, rule, or task was created.<br />-   To run **\/usr\/bin\/vmstat** for the **Run VMStat** task.|
|Privileged profile|<ul><li>To log the UNIX or Linux computer on to the network, authenticated by the PAM. Must have the ability to run a background shell \(not connected to a TTY\). Interactive logons are not required. In the case of an account that is elevated by using `sudo`, this requirement applies to the account before it is elevated.</li><li>To fully run any shell command line that was specified as privileged when a command\-line monitor, rule, or discovery was created.</li><li>To have the following log file monitoring capabilities:<br /><br /><ul><li>To read the log file to be monitored.<br /><br />        By default, log files such as Syslog are usually set to be readable only by root, and accounts assigned to this profile must be able to read these files. Instead of giving accounts full root privileges, the log file permissions could be changed to grant read access to a secure group, and accounts made a member of that group. Note that if the log file is periodically rotated, you must ensure that the rotation procedure maintains the group permissions.</li><li>To read any log file that was specified as privileged when a custom log file monitor was created.</li><li>To run **\/opt\/microsoft\/scx\/bin\/scxlogfilereader**.</li></ul></li><li>To run tasks, recoveries, and diagnostics. These requirements must be met only if the [!INCLUDE[om12short](./Token/om12short_md.md)] operator explicitly decides to run them.<br /><br /><ul><li>Many recoveries include stopping and restarting a daemon process. These recoveries require the ability to run the service control interfaces \(such as **\/etc\/init.d** for Linux, and **svcadm** for Solaris\) in order to stop and restart it. Such service control interfaces typically require the ability to run the **kill** command against the daemon process and to run other basic UNIX and Linux commands.</li><li>The requirements for other tasks, recoveries, and diagnostics depend on the details of that particular action.</li></ul></li></ul>|
|Agent maintenance profile, and for accounts used to install agents for initial monitoring.|<ul><li>To log the UNIX or Linux computer on to the network by using Secure Shell \(SSH\), authenticated by the PAM. Must have the ability to run a background shell \(not connected to a TTY\). Interactive logons are not required. In the case of an account that is elevated by using `sudo`, this requirement applies to the account before it is elevated.</li><li>To run the system package installation program, such as **rpm** on Linux, to install the [!INCLUDE[om12short](./Token/om12short_md.md)] agent.</li><li>To read and write the following directories, and to create them and any subdirectories under them if they do not exist:<br /><br /><ul><li>**\/opt**</li><li>**\/opt\/microsoft**</li><li>**\/opt\/microsoft\/scx**</li><li>**\/etc\/opt\/microsoft\/scx**</li><li>**\/var\/opt\/microsoft\/scx**</li></ul></li><li>To run the **kill** command against the running [!INCLUDE[om12short](./Token/om12short_md.md)] agent processes.</li><li>To start the [!INCLUDE[om12short](./Token/om12short_md.md)] agent.</li><li>To add and remove a system daemon, including the [!INCLUDE[om12short](./Token/om12short_md.md)] agent, by using platform tools to do so.</li><li>To run basic UNIX and Linux commands, such as **cat**, **ls**, **pwd**, **cp**, **mv**, **rm**, **gzip** \(or equivalent\).</li></ul>|

## See Also
[How to Set Credentials for Accessing UNIX and Linux Computers](./How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md)
[Accessing UNIX and Linux Computers in Operations Manager](./Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[How to Configure sudo Elevation and SSH Keys](./How-to-Configure-sudo-Elevation-and-SSH-Keys.md)
[Credentials You Must Have to Access UNIX and Linux Computers](./Credentials-You-Must-Have-to-Access-UNIX-and-Linux-Computers.md)
[Configuring SSL Ciphers](./Configuring-SSL-Ciphers.md)


