---
title: Plan for data recovery
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8b51abb-db11-4d5e-8b70-a1a5bdfbde5f
---
# Plan for data recovery
[!INCLUDE[sc2012](./Token/sc2012_md.md)] \- [!INCLUDE[dpm2012sp1long](./Token/dpm2012sp1long_md.md)] implements recovery by retrieving backed\-up data. To recover data, you select a recovery point \(snapshot\) from which to retrieve data. Each recovery point\-is a point\-in\-time copy of backed up data. The general process of backup and recovery is as follows:

1.  **Create initial replica**—When you configure a resource as a member of a protection group, you are prompted to create an initial replica of the data. This initial replica creates a baselines copy of the protected data. This baseline replica is used to create a recovery point, and when DPM synchronizing data changes and differences.

2.  **Synchronize data**—DPM checks the data source for changes, and then updates the replica. Learn more about

3.  **Create recovery point**—As DPM synchronizes, it creates recovery points from which data can be retrieved if needed. [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] creates recovery points for file data by taking a shadow copy of the replica on a schedule that you configure. For application data, each synchronization and express full backup creates a recovery point.

4.  **Recover data**—You recover data from available recovery points by using the Recovery Wizard in [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console. When you select a data source and point in time from which to recover, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] notifies you if the data is on tape, whether the tape is online or offline, and which tapes are needed to complete the recovery.


