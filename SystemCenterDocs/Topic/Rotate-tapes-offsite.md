---
title: Rotate tapes offsite
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cfa89de-8742-4f1f-bb6c-0ab25276acfc
---
# Rotate tapes offsite
DPM Administrator Console indicates when a tape in the library should be removed and stored in your archive location by displaying a green icon in the **Offsite Ready** column. You can also view all tapes ready to be stored offsite in the Tape Management Report. The Tape Management Report lists tapes that will be due for offsite storage in the upcoming period selected for the report.

A tape can be marked as **Offsite Ready** for one of three reasons.

|Reason|Description|
|----------|---------------|
|Tape is full|When a tape is full, DPM marks it as **Offisite Ready**.|
|Expired data set|A data set on the tape has expired.|
|Write Period Ratio has been crossed|Write Period Ratio is calculated as \(Time of first backup \+ 15% of retention range\).|

When the data on a tape expires, return the tape to the tape library. Expired tapes not returned to the tape library are marked as "overdue" in the Tape Management Report. Overdue tapes expired during an earlier reporting period. Expired tapes should be returned to the tape library for reuse.

