---
ms.assetid: 
title: Sudoers Templates for Elevation in UNIX/Linux Monitoring
titlesuffix: Microsoft System Center Operations Manager
description: This article provides sudoers file templates for monitoring Unix and Linux operating systems with Microsoft System Center Operations Manager.
author: sepaugh
ms.author: lornesepaugh
manager: benvan
ms.date: 11/01/2024
ms.topic: reference
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Sudoers templates for elevation in UNIX/Linux monitoring



Effective monitoring of UNIX or Linux operating systems requires some elevated permissions on the client system for both monitoring and maintenance tasks. There are sudoers configuration templates provided in this article for baseline operability.

## Introduction

In order to use sudo-enabled accounts for monitoring with Operations Manager, configurations must be put into place to authorize elevation for RunAs Accounts using sudo. General requirements for the accounts used by Operations Manager with sudo elevation are:

- The accounts must have RequireTTY disabled as a default parameter.
- The accounts must be configured to elevate with NOPASSWD.
- The accounts must have the "lecture" that typically is shown when logging in, and when elevating using sudo, disabled.

The provided templates specify the commands that allow the configured RunAs Accounts to execute tasks that require elevated permissions such as:

- Installing the agent
- Upgrading the agent
- Uninstalling the agent
- Monitoring system logs
- Restarting the agent services
- Facilitating the creation of authentication certificates

> [!NOTE]
> Commands and requirements are **not** the same across all UNIX/Linux distributions or versions, ensure you have the correct template for your Operating System.
>
> Don't see your OS? Refer to the [Supported UNIX and Linux operating system versions](plan-supported-crossplat-os.md) page for supported distributions.

## Using the templates

Select the appropriate template for your Operating System and replace the example accounts with your RunAs Account usernames, include are other organizational customizations if necessary.

In each template there are two accounts defined and maps to standard RunAs Accounts as:

| RunAs Account | Username |
|---------------|----------|
| UNIX/Linux Action Account | scomuser |
| UNIX/Linux Maintenance Account | scomadm |

Once updated with the correct usernames and any extra modifications, the template must be added to the client system's sudoers configuration. There are typically two ways to add sudo configurations, either by directly modifying the `/etc/sudoers` or `/etc/sudo.conf` file (depending on the OS), or by adding a "drop in" file under `/etc/sudoers.d` (ex. `/etc/sudoers.d/scom`). This article doesn't go into detail on how to fully configure sudo itself. For more information, see the documentation provided by the vendor for your specific operating system.

::: moniker range="< sc-om-2022"

## AIX

[!INCLUDE [sudoers-aix.md](includes/sudoers-aix.md)]
[!INCLUDE [sudoers-hpux.md](includes/sudoers-hpux.md)]

::: moniker-end

## Red Hat Enterprise Linux (RHEL)

::: moniker range=">= sc-om-2019"

> [!IMPORTANT]
> Beginning with version 8, Red Hat Enterprise Linux falls under [Universal Linux](#universal-linux).

::: moniker-end

::: moniker range="< sc-om-2022"

### RHEL 6

[!INCLUDE [sudoers-rhel6.md](includes/sudoers-rhel6.md)]

::: moniker-end

### RHEL 7

[!INCLUDE [sudoers-rhel7.md](includes/sudoers-rhel7.md)]

::: moniker range="< sc-om-2022"

## Solaris

[!INCLUDE [sudoers-solaris.md](includes/sudoers-solaris.md)]

::: moniker-end

## SUSE Linux Enterprise Server (SLES)

::: moniker range=">= sc-om-2019"

> [!IMPORTANT]
> Starting with version 15, SUSE falls under [Universal Linux](#universal-linux).

::: moniker-end

[!INCLUDE [sudoers-sles.md](includes/sudoers-sles.md)]

## Universal Linux

Universal Linux encompasses both Debian and Red Hat based operating systems and is where to find the latest supported Linux operating systems and distributions. For a list of distros that fall under this class type, refer to: [Supported UNIX and Linux Operating System Versions](/SystemCenterDocs/scom/plan-supported-crossplat-os.md#universal-linux-debian-package-1).

[!INCLUDE [sudoers-universallinux.md](includes/sudoers-universallinux.md)]

## Other commands

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

There should be no quotes around the command as only the shell recognizes them, sudo doesn't.

## Troubleshooting

### Sudo error log

One of the best ways to troubleshoot authentication failures related to sudoers configurations can be to inspect the sudo log on the agent host.

- For RedHat based operating systems, the default log location is `/var/log/secure`.
- For Debian based operating systems, the default log location is `/var/log/auth.log`.

Check the `/etc/sudoers` file for the `logfile` parameter to see where the log is currently being written to if using a different operating system or customized log location.

### Password prompts and timeouts

By default, sudo prompts for a password if a command isn't configured with `NOPASSWD` for the user, there's no functionality to automatically input passwords when prompted like this, and breaks monitoring. To prevent extended issues if `NOPASSWD` isn't configured for a command, the recommendation is to configure the following option in sudoers for the user account:

```bash
Defaults:scomuser passwd_tries = 1, passwd_timeout = 1
```

This example sets a one-minute password prompt timeout for the user *scomuser*, which allows the command to fail quickly if a sudo configuration problem exists.

### Password errors or other authentication failures

For guidelines on password and authentication configurations, see [Planning Security Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).
