---
ms.assetid: 
description: include file to summarize the release notes for System Center 2022 - Service Management Automation
ms.topic:  include
author: jyothisuri
ms.author: jsuri
ms.service:  system-center
ms.subservice: service-management-automation
keywords:
ms.date: 06/09/2022
title:  include file
---

## SMA 2022 release notes

The following issues have been fixed in SMA 2022:

- Improper handling of the lifecycle resulted in increased memory usage due to idle Sandbox processes that were *stalled* and couldn't be killed easily.

- The jobs were going into *Suspended* or *Stopping* state and the associated Sandbox processes would become unresponsive.