---
ms.assetid: 03be2a03-3c30-418f-8c5c-169744ac864f
title: Set up storage classifications in the VMM 2016 fabric
description: This article describes how to set up storage classifications in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---
# Set up storage classifications in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Use storage classifications to abstract storage devices in the System Center - Virtual Machine Manager (VMM) fabric. You classify storage devices with similar characteristics, and assign these classifications, rather than specific storage devices, to hosts and clusters. The host and cluster can then use any available storage n the classification.

Classifications are often based on storage types or performance characteristics. For example, you could create:

**Name** | **Description**
--- | ---
**GOLD** | Storage pool based on solid-state drives (SSDs) that delivers high performance for I/O intensive applications
**SILVER** | Fibre Channel Serial Attached SCSI (SAS) storage (RAID 5)
**BRONZE** | iSCSI Serial ATA (SATA) storage (RAID 5)

## Create classifications:

1.  Click **Fabric** > **Storage**, right-click **Classification and Pools** > **Create Classification**.
2.  In **New Classification**, enter a name and description > **Add**.

## Next steps

[Add storage devices](storage-device.md) to the VMM fabric.
