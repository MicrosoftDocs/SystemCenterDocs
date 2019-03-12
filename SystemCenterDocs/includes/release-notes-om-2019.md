---
title: include file
description: include file to summarize the release notes for Operations Manager 2019.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 03/14/2019
ms.prod: system-center
ms.assetid: 56adc06e-4317-4622-83f2-cc44a5f40c78
ms.technology: operations-manager
ms.topic: include
---

## Operations Manager 2019 release notes

The following sections summarize the release notes for Operations Manager 2019 and include the known issues and workarounds.

## Health Service runs with Log on type as *Service* by default

**Description:**
With Operations Manager 2019, *Log on as a Service* feature is enabled by default. This change impacts all the service accounts and Run As accounts. With this change, all these accounts must have *Log on as a Service* permission.  

**Workaround:** Enable log on as a service. [Learn more](../scom/enable-service-logon.md)

## User experience changes in maintenance mode

**Description**: The following are the user experience changes with Operations Manager 2019 maintenance mode, applicable to both Windows and Linux\Unix monitoring:

- As an entity enters maintenance mode, monitor-based active alerts on it will be automatically resolved.  In earlier releases, these alerts get automatically resolved when the entity exits the  maintenance mode.

- On-demand monitors and regular monitors now behave similarly when target entity enters and exits the maintenance mode.

**Workaround**: None

## Support for x64 components

**Description**:  Operations Manager 2019 supports only x64 components, x86 components are not supported.
If you try to push install the agent from the console to a x86 computer, the following error message appears:

*The system cannot find the path specified*.

**Workaround**:  None  

## Upgrade to reporting server fails the prerequisites check

**Description**: While attempting to perform an upgrade of System Center 2016/1801/1807 - Operations Manager reporting server to version 2019, the prerequisites check reports the following error: 

*Management Server Upgraded Check - The management server to which this component reports, has not been upgraded. and the upgrade cannot proceed*.

This error occurs in a distributed management group scenario, where the reporting server is on a server, which is different from one or more management servers in the management group.

**Workaround**: Install the System Center 2016/1801/1807 - Operations Manager Operations console on the server that is hosting the reporting server role, and then retry upgrading the reporting server role to version 2019. Once the upgrade is successful, you can uninstall the upgraded Operations console from the reporting server.

## Internet Explorer compatibility view

**Description**: The HTML5 Web console does not support Internet Explorer compatibility View.  

**Workaround**: None

## OpenSSL 1.1.0 version support

**Description**: On Linux platforms, OpenSSL 0.9.8 support is dropped.

**Workaround**: We have added support for OpenSSL 1.1.0.
