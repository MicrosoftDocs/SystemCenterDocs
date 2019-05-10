---
title: include file
description: include file that summarizes the release notes for Operations Manager 2019.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 05/10/2019
ms.prod: system-center
ms.assetid: 56adc06e-4317-4622-83f2-cc44a5f40c78
ms.technology: operations-manager
ms.topic: include
---

## Operations Manager 2019 release notes

The following sections summarize the release notes for Operations Manager 2019 and include the known issues and workarounds.

## Health Service with Log on type as *Service* by default

**Description:**
With Operations Manager 2019, *Log on as a Service* feature is enabled by default. This change impacts all the service accounts and Run As accounts, they must have *Log on as a Service* permission.  

**Workaround:** Enable log on as a service permission for these accounts. [Learn more](../scom/enable-service-logon.md).

## User experience changes in maintenance mode

**Description**: The following are the user experience changes with Operations Manager 2019 maintenance mode. These changes are applicable to both Windows and Linux\Unix monitoring:

- As an entity enters the maintenance mode, monitor-based active alerts on it will be automatically resolved.  In earlier releases, these alerts get automatically resolved when the entity exits the  maintenance mode.

- On-demand monitors and regular monitors now behave similarly when target entity enters and exits the maintenance mode.

**Workaround**: None

## Support for x64 components

**Description**:  Operations Manager 2019 supports only x64 components, x86 components aren't supported.
If you try to push install the agent from the console to a x86 computer, the following error message appears:

*The system cannot find the path specified*.

**Workaround**:  None  

## Upgrade to reporting server fails the prerequisites check

**Description**: While attempting to do an upgrade of System Center 2016/1801/1807 - Operations Manager reporting server to version 2019, the prerequisites check reports the following error: 

*Management Server Upgraded Check - The management server to which this component reports, has not been upgraded. and the upgrade cannot proceed*.

This error occurs in a distributed management group scenario, where the reporting server is on a server that is  different from one or more management servers in the management group.

**Workaround**: Install the System Center 2016/1801/1807 - Operations Manager Operations console on the server that is hosting the reporting server role, and then retry upgrading the reporting server role to version 2019. Once the upgrade is successful, you can uninstall the upgraded Operations console from the reporting server.

## Internet Explorer compatibility view

**Description**: The HTML5 Web console doesn't support Internet Explorer compatibility View.  

**Workaround**: None

## OpenSSL 1.1.0 version support

**Description**: On Linux platforms, OpenSSL 0.9.8 support is dropped.

**Workaround**: We have added support for OpenSSL 1.1.0.

## Performance monitoring for VMM server fails with Access denied message
**Description**: Service users do not have permission to access VirtualMachineManager-Server/Operational event log.
**Workaround**: Change the Security Descriptor for operational event log registry with the command below, and then restart event log service and health log service.

```
reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Channels\Microsoft-VirtualMachineManager-Server/Operational /v ChannelAccess /t REG_SZ /d O:BAG:SYD:(D;;0xf0007;;;AN)(D;;0xf0007;;;BG)(A;;0xf0007;;;SY)(A;;0x7;;;BA)(A;;0x3;;;NS)(A;;0x1;;;IU)(A;;0x1;;;SU)"
```

This command will add the service user to the list of allowed users, who can access VirtualMachineManager-Server/Operational event log.

## Operations Manager 2019 does not support HPUX library  

**Description**: Operations Manager 2019 does not support HPUX. However, HPUX library is available in the list of management packs delivered for Operations Manager 2019.

**Workaround**: Ignore this, HPUX is not supported in 2019.
