---
title: Operating System Issues
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5adf948f-c85b-4851-a6fa-0213189eeb16
---
# Operating System Issues
This topic describes issues that are specific to UNIX and Linux operating systems.

## Incorrect Reports of Shared Resources from a Solaris 10\-Based Server
When you monitor a Sun Solaris 10\-based server that is configured to use zones, Operations Manager might appear to incorrectly report shared resources such as a physical disk or a network adapter. This behavior occurs by design.

On a Solaris 10\-based server that is configured to use zones, Operations Manager does not differentiate shared resources such as a physical disk or a network adapter. For any local zone that shares a global zone resource, Operations Manager does not report the shared resource. Only one instance of each resource is monitored on each Solaris 10\-based server. If two network adapters exist on a Solaris 10\-based server, and one is attached to the global zone while the second is shared between two local zones, the first enumerated local zone reports the shared resource. The second local zone will have no data for the shared resource.

In Operations Manager, the behavior of a Solaris 10\-based server that is deployed in a virtual machine might differ slightly from the behavior of a Solaris 10\-based server that is deployed on a physical computer. Each network adapter that exists in a virtual machine appears to the Solaris 10\-based server as a separate physical resource. If uniquely defined network adapters are attached to each zone that is configured on the Solaris\-based server, Operations Manager collects data for each network adapter.

## Agent Providers Might Fail If the Solaris Computer’s File Descriptor Limit is Reached by the Process
On a monitored Solaris computer with a large number of monitored objects \(such as file systems or processors\), you may observe unreliable behavior of the Solaris agent. Symptoms can include file systems, disks, or other objects not being discovered.  This can be caused by the agent process running out of available File Descriptors \(FD\).

To determine if an issue is the result of File Descriptor limits, inspect the agent log file: \/var\/opt\/microsoft\/scx\/log\/scx.log. If any error messages in the log contain the text: errno \= 24 \(Too many open files\), a FD limit issue should be suspected.

To resolve this issue, perform the following steps:

1.  Modify the scx\-cimd startup script at \/opt\/microsoft\/scx\/bin\/tools\/scx\-cimd \(Solaris 10 or Solaris 11\) or \/etc\/init.d\/scx\-cimd \(Solaris 9\). Find the section of the script with the following lines:

    ```
    start)
        # Start daemon
        echo "Starting $DESC"
        $DAEMON $OPTIONS -d
        exit $?
        ;;
    ```

    Modify this section to include a ulimit –n 1024 command, prior to the $DAEMON $OPTIONS –d line, where “1024” is the new process limit for File Descriptors.

    ```
    start)
        # Start daemon
        echo "Starting $DESC"
        ulimit –n 1024
        $DAEMON $OPTIONS -d
        exit $?
        ;;
    ```

2.  Restart the agent:

    ```
    scxadmin -restart
    ```

3.  If the issue persists, try the configuration again with a File Descriptor limit of 2048, and then restart the agent. If the process continues to exhaust File Descriptors with the 2048 limit set, contact support.

## See Also
[Using Templates for Additional Monitoring of UNIX and Linux](../Topic/Using-Templates-for-Additional-Monitoring-of-UNIX-and-Linux.md)
[Troubleshooting UNIX and Linux Monitoring](../Topic/Troubleshooting-UNIX-and-Linux-Monitoring.md)
[Accessing UNIX and Linux Computers in Operations Manager](../Topic/Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[Required Capabilities for UNIX and Linux Accounts](../Topic/Required-Capabilities-for-UNIX-and-Linux-Accounts.md)
[Management Pack Issues](../Topic/Management-Pack-Issues.md)
[Certificate Issues](../Topic/Certificate-Issues.md)
[Logging and Debugging](../Topic/Logging-and-Debugging.md)
[Managing Certificates for UNIX and Linux Computers](../Topic/Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Managing Resource Pools for UNIX and Linux Computers](../Topic/Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](../Topic/Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)

