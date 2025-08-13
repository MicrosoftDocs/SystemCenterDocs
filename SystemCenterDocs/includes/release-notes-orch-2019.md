---
ms.assetid: 3f002367-963a-4a35-bcd5-b2dd79b58ea2
description: Include file to summarize the release notes for System Center 2019 - Orchestrator.
ms.topic:  Include
author: jyothisuri
ms.author: jsuri
ms.service:  system-center
ms.subservice: Orchestrator
keywords:
ms.date: 03/19/2024
title:  include file
---

## Orchestrator 2019 UR6 release notes

The following sections summarize the release notes for Orchestrator 2019 UR6, and include the known issues and workarounds.

For the problems fixed in UR6 and the installation instructions for UR6, see the [KB article](https://support.microsoft.com/kb/5035767).


### New Web console doesn't take zero (0) as the input parameter

**Description**: New web console doesn't take zero as the input parameter.

**Workaround**: Change the data type of input parameter to String.

### Web Console requires third party cookies when opening console via localhost or FQDN  

**Description**: Web Console requires third party cookies **enabled** when opening console via localhost or FQDN, but not with Netbios name.

**Workaround**: Add **Allow 3rd party cookies** to localhost and FQDN in Edge settings on all client machines.

## Orchestrator 2019 release notes

The following are known issues in System Center 2019 - Orchestrator.

- See [KB article #4533414](https://support.microsoft.com/help/4533414) for issues fixed in Orchestrator UR1.
- See [KB article #4569536](https://support.microsoft.com/help/4569536) for issues fixed in Orchestrator UR2.
- See [KB article #4599686](https://support.microsoft.com/help/4599686) for issues fixed in Orchestrator UR3.

### New Web API and Console (without Silverlight)

Follow the instructions in the [announcement blog post](https://techcommunity.microsoft.com/t5/system-center-blog/a-brand-new-web-console-for-orchestrator-2019/ba-p/3040427) to download and install the new components.

The new components can work alongside the original 2019 Web Service and Console.

### Other known issues

#### Orchestrator Web Console isn't compatible with the Microsoft Edge web browser

**Description**: You can't open the Orchestrator web console with the Microsoft Edge web browser.

**Workaround**: Open the Orchestrator web console with Internet Explorer.

> [!TIP]
> New version of the Web API and Orchestrator Console have been released that doesn't depend on Silverlight. Follow instructions in the [announcement blog post](https://techcommunity.microsoft.com/t5/system-center-blog/a-brand-new-web-console-for-orchestrator-2019/ba-p/3040427) to download and install them.
