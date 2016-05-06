---
title: Management Pack Issues
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f135eb4-49d0-46a6-a717-77c1ee3bbed7
---
# Management Pack Issues
This topic describes issues that are specific to management packs and modules.

## ExecuteCommand Does Not Support Pipeline Operators or Aliases
When you use an alias or a pipeline operator with the *ExecuteCommand* parameter, the command fails. The *ExecuteCommand* parameter does not support the pipeline operator, aliases, and shell\-specific syntax.

In System Center Operations Manager management packs that are designed to manage UNIX and Linux computers, the *ExecuteCommand* parameter does not start a shell process, causing the custom action to fail.

For each of the following custom action types, you specify how the command arguments are invoked by using either the *ExecuteCommand* parameter or the *ExecuteShellCommand* parameter:

-   Microsoft.Unix.WSMan.Invoke.ProbeAction

-   Microsoft.Unix.WSMan.Invoke.WriteAction

-   Microsoft.Unix.WSMan.Invoke.Privileged.ProbeAction

-   Microsoft.Unix.WSMan.Invoke.Privileged.WriteAction

The *ExecuteCommand* parameter passes the command\-line arguments to the console without starting a shell process.

The *ExecuteShellCommand* parameter passes the command arguments to a shell process using the user's default shell; this shell supports pipeline, aliases, and shell\-specific syntax.

> [!NOTE]
> The *ExecuteShellCommand* parameter uses the default shell of the user who is running the command. If you require a specific shell, use the *ExecuteCommand* parameter, and prefix the command arguments with the required shell.

The following examples show how to use the *ExecuteCommand* and *ExecuteShellCommand* parameters:

-   To pass the command\-line arguments to the console without starting a shell process:

    `<p:ExecuteCommand_INPUT xmlns:p="http://schemas.microsoft.com/wbem/wscim/1/cim-schema/2/SCX_OperatingSystem"> <p:Command> service syslog status </p:Command> <p:timeout>10</p:timeout> </p:ExecuteCommand_INPUT>`

-   To pass the command\-line arguments to a shell process that references an explicit shell:

    `<p:ExecuteCommand_INPUT xmlns:p="http://schemas.microsoft.com/wbem/wscim/1/cim-schema/2/SCX_OperatingSystem"> <p:Command> /bin/sh ps -ef syslog | grep -v grep </p:Command> <p:timeout>10</p:timeout> </p:ExecuteCommand_INPUT>`

-   To pass the command arguments to a shell process that uses the user's default shell:

    `<p:ExecuteShellCommand_INPUT xmlns:p="http://schemas.microsoft.com/wbem/wscim/1/cim-schema/2/SCX_OperatingSystem"> <p:Command> uptime |  awk '{print $10}' |awk -F"," '{print $1}' </p:Command> <p:timeout>10</p:timeout> </p:ExecuteShellCommand_INPUT>`

## See Also
[Using Templates for Additional Monitoring of UNIX and Linux](./Using-Templates-for-Additional-Monitoring-of-UNIX-and-Linux.md)
[Troubleshooting UNIX and Linux Monitoring](./Troubleshooting-UNIX-and-Linux-Monitoring.md)
[Accessing UNIX and Linux Computers in Operations Manager](./Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[Required Capabilities for UNIX and Linux Accounts](./Required-Capabilities-for-UNIX-and-Linux-Accounts.md)
[Certificate Issues](./Certificate-Issues.md)
[Operating System Issues](./Operating-System-Issues.md)
[Logging and Debugging](./Logging-and-Debugging.md)
[Managing Certificates for UNIX and Linux Computers](./Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Managing Resource Pools for UNIX and Linux Computers](./Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](./Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)


