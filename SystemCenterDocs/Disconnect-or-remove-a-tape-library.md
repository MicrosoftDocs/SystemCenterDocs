---
title: Disconnect or remove a tape library
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bfc8927a-b3ce-42c5-ac06-75f0ae4b1308
---
# Disconnect or remove a tape library
If you physically disconnect a tape library or stand\-alone tape drive, or physically remove a drive from inside a library that is associated with a protection group, DPM Administrator Console displays the disconnected or removed tape library or stand\-alone tape drive as offline.

If you disconnect or remove a tape library or stand\-alone tape drive that is not associated with a protection group, the entry for the tape library or stand\-alone tape drive is removed from DPM Administrator Console during the daily inventory or when rescan runs, whichever occurs first.

If you remove a tape library that is associated with a protection group and you do not intend to bring the tape library online again, you should modify the protection group to specify a different tape library. When all protection groups that were associated with the tape library that you removed are associated with other tape libraries, the entry for the tape library or stand\-alone tape drive will be removed from DPM Administrator Console during the daily inventory or when rescan runs, whichever occurs first.


