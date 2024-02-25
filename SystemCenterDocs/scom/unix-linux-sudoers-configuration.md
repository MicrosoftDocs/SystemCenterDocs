---
ms.assetid: 
title: Configuring sudo elevation for UNIX or Linux Monitoring
description: This article provides sudoers file templates for monitoring Unix and Linux operating systems with Microsoft System Center Operations Manager (SCOM).
author: sepaugh
ms.author: lornesepaugh
manager: benvan
ms.date: 02/24/2024
ms.custom: na
ms.product: msc-operations-manager
ms.topic: reference
---

# Configuring sudo elevation for Unix/Linux monitoring

Effective monitoring of UNIX or Linux operating systems requires some elevated permissions on the client system for both monitoring and maintenance tasks. Provided here are templates for use in configuring sudo for baseline monitoring.

## Introduction

In order to use sudo-enabled accounts for monitoring with Operations Manager, the sudo configurations must be put into place to authorize elevation for the selected Run As Account using sudo. General requirements for the accounts used by Operations Manager with sudo elevation are:

- The account must have RequireTTY disabled as a default parameter.
- The accounts must be configured to elevate with NOPASSWD.
- The accounts must have the "lecture" that typically is shown when logging in elevating using sudo disabled.

Refer to the [Supported UNIX and Linux operating system versions](plan-supported-crossplat-os.md) page for supported distributions.

## Configuring sudoers files

There are typically two ways to add sudo configurations, by directly modifying the `/etc/sudoers` file, or by adding a "drop in' file under `/etc/sudoers.d`. For easy maintainability and distribution, consider adding a new file under `/etc/sudoers.d` and have `#includedir /etc/sudoers.d` as part of the main sudoers file, this article doesn't go into detail on how to fully configure sudo. For more information about configuring sudo, see the vendor for your specific operating system.

## Sudoers templates

> [!NOTE]
> Requirements are **not** the same across all UNIX/Linux distributions or versions, ensure you have the correct template for your Operating System.

In each template there are two accounts defined, and maps to standard RunAs Accounts as:

| RunAs Account | Username |
|---------------|----------|
| Unix/Linux Action Account | scomuser |
| Unix/Linux Maintenance Account | scomadm |

::: moniker range="< sc-om-2022"

### AIX

[!INCLUDE [sudoers-aix.md](includes/sudoers-aix.md)]
[!INCLUDE [sudoers-hpux.md](includes/sudoers-hpux.md)]

::: moniker-end

### Red Hat Enterprise Linux (RHEL)

Beginning with major version 8, Red Hat Enterprise Linux is contained within the "[Universal Linux](#universal-linux)" packages.

::: moniker range="< sc-om-2022"

#### RHEL 6

[!INCLUDE [sudoers-rhel6.md](includes/sudoers-rhel6.md)]

::: moniker-end

#### RHEL 7

[!INCLUDE [sudoers-rhel7.md](includes/sudoers-rhel7.md)]

### Solaris

[!INCLUDE [sudoers-solaris.md](includes/sudoers-solaris.md)]

### SUSE Linux Enterprise Server (SLES)

Starting with version 15, SUSE is contained within the [Universal Linux](#universal-linux) packages.

[!INCLUDE [sudoers-sles.md](includes/sudoers-sles.md)]

### Universal Linux

Universal Linux encompasses both Debian and Red Hat based operating systems, and is the class that contains configurations for the latest supported Linux operating systems and distributions.

[!INCLUDE [sudoers-universallinux.md](includes/sudoers-universallinux.md)]

## Other Commands

When using the **ExecuteShellScript** method to run elevated scripts, add the following line your sudoers file for your user:

```bash
scomuser ALL=(root) NOPASSWD: /etc/opt/microsoft/scx/conf/tmpdir/scx*
```

This line is required as the ExecuteShellScript method copies the contents of the elevated script to a temporary file with a randomly generated filename in `tmpdir` and execute it from there.

When using the **ExecuteShellCommand** method to run elevated commands, add something like this in your sudoers file:

- `/bin/sh` is the default shell of the user running the command, and (in this example).
- `/usr/bin/vmstat -c` is the command you want to run.

```bash
scomuser ALL=(root) NOPASSWD: /bin/sh -c /usr/bin/vmstat -c
```

There should be no quotes around the command as sudo doesn't recognize them, only the shell itself.

```bash

```

## Troubleshooting

### Sudo log

One of the best ways to troubleshoot authentication failures, related to sudoers configuration, can be to inspect the sudo log on the agent host.

- For RedHat based operating systems, the default log location is `/var/log/secure`.
- For Debian based operating systems, the default log location is `/var/log/auth.log`.

Check the `/etc/sudoers` file for the `logfile` parameter to see where the log is currently being written to, if using a different operating system or a customized log location.

### Password prompts and timeouts

By default, sudo prompts for a password if a command isn't configured with `NOPASSWD` for the user, there's no functionality to automatically input passwords when prompted like this, and breaks monitoring. To prevent extended issues if `NOPASSWD` isn't configured for a command, the recommendation is to configure the following option in sudoers for the user account:

```bash
Defaults:scomuser passwd_tries = 1, passwd_timeout = 1
```

This example sets a one-minute password prompt timeout for the user *scomuser*, which allows the command to fail quickly if a sudo configuration problem exists.

### Password errors or authentication failures

For guidelines on password and authentication configurations, see [Planning Security Credentials for Accessing Unix and Linux Computers](manage-security-create-crossplat-credentials.md).
