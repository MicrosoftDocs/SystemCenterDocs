---
ms.assetid: 
title: Include file
description: Include file to summarize the release notes for VMM 2025.
author: Karthik K R
ms.author: krkarthik
ms.date:  07/27/2026
ms.topic:  include
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.update-cycle: 1095-days
---

## VMM 2025 release notes

The following sections summarize the release notes for VMM 2025 and include the known issues and workarounds.

- For issues fixed in 2025 UR1, [see the KB article for UR1](https://support.microsoft.com/kb/5068308).

## Known issues

### VMM Console to guest VM interaction with non-English(US) languages

When the default language configured in the guest VM and the VMM console is not English (US), copying text from the VMM console into the guest VM might be impacted. This limitation primarily impacts the VM log in functionality while copy-pasting password from the VMM console into guest VM to log in to the VM. Changing the language to English (US) by using the keyboard language icon in the VM log in page temporarily circumvents this issue.
