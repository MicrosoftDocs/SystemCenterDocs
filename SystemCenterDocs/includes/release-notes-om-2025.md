---
title: include file
description: Include file that summarizes the release notes for Operations Manager 2025.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 01/19/2026
ms.service: system-center
ms.assetid:
ms.subservice: operations-manager
ms.topic: include
---

## Orchestrator 2025 UR1 Release notes

The following sections summarize the release notes for Operations Manager 2025 UR1, and include the known issues and workarounds.

For the problems fixed in UR1 and the installation instructions for UR1, see the [KB article](https://support.microsoft.com/kb/5068304).

### Enabling TLS 1.3 causes some functionality issues

**Description**: Agents connected through the Gateway aren't sending heartbeats to the Management Server. 

**Workaround**:
Disable TLS 1.3 in the Windows registry until a permanent fix is available and update the following registry settings on both the Management Server and the Gateway Server.

`[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Client]`
`"Enabled"dword:00000000`
`"DisabledByDefault"=dword:00000001`

`[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Server]`
`"DisabledByDefault"=dword:00000001`
`"Enabled"=dword:00000000`

## Operations Manager 2025 release notes

This article summarizes the release notes for Operations Manager 2025.

- Fixed broken behavior of Web Console where allow-popups and allow-forms settings weren't added after applying security changes.
- Fixed failure of favorite reports with `HttpParseException` in Web Console.
