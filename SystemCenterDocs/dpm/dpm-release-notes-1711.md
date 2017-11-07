---
ms.assetid:
title: Release Notes for System Center DPM 1711
description: These release notes provide general information about the DPM 1711 release.
author: markgalioto
ms.author: markgal
manager: carmonm
ms.date: 11/08/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: data-protection-manager
ms.topic: article
monikerRange: 'sc-dpm-1711'
---

# Release Notes for System Center Data Protection Manager (DPM) Technical Preview 1711

The following note is the known issue and steps to mitigate the issue. This note applies to System Center Data Protection Manager (DPM) Technical Preview 1711.  

## Installing the DPM agent on Windows Server may require a reboot

**Description**: Installing or updating a DPM agent on a Windows Server may require a reboot.

**Workaround**: To understand if the production server may require a reboot when the agent is updated, check the version of the *Microsoft Visual C++ 2012 Redistributable(x64)*. If the version is below 11.0.51106, the agent installation process tries to update the agent, which can cause the server to reboot. Avoid pushing the agent to these servers. 

If you have a server whose version is less than 11.0.51106, on the production server, open the DPM setup folder(<DPM Installation Path>\DPM\ ProtectionAgents\AC\<DPM Version>\amd64), pick *vcredist2012_x64*, and install it manually. It will prompt for a reboot and then you will have control whether to reboot or not. 

After manually installing the update, you can push the agents.
