---
title: Set tape catalog retention for a protection group
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39cb94e6-15ac-43a0-ada3-50f078bf312d
---
# Set tape catalog retention for a protection group
DPM maintains metadata for each tape in a database, referred to as the *tape catalog*. You can manage the retention settings for the tape catalog to determine when the catalog is *pruned*, which consists of removing entries from the catalog. DPM automatically prunes the catalog when the retention range for the protection group expires, but you can direct DPM to prune the catalog for all protection groups sooner to reduce the size of the database as follows:

1.  In DPM Administrator Console, go to the **Protection** view and select a protection group.

2.  Click **Specify tape catalog retention**. To prune the catalog when the retention range expires, select **Prune catalog when protection group retention range expires**. To prune the catalog for a specific tape duration, select **Prune catalog for tapes older than**, and then select the tape duration that you want to use.

    Note that you can’t retain catalog data longer than the retention range for the protection group.

3.  If you want DPM to alert you when the DPM database reaches a specific size, in the **DPM Database** section, select **Alert me when the DPM database size reaches**, and then specify the size of the database.


