---
title:  System Center - Data Protection Manager volume to volume migration
description: This article describes volume to volume migration.
manager: vvithal
ms.topic: article
author: v-anesh
ms.prod: system-center
keywords:
ms.date: 06/16/2020
ms.technology: data-protection-manager
ms.assetid: 6595b781-554d-4807-b035-d0eccd35deb3
ms.author: v-anesh
monikerRange: '>=sc-dpm-2019'
---

# Optimized volume to volume migration

> [!NOTE]
> This feature is applicable from UR2 and later.

The optimized volume to volume migration allows you to move data sources to the new volume much faster. The enhanced migration process migrates only active backup copy (Active Replica) to the new volume. All the new recovery points are created on the new volume while existing recovery points are maintained on the existing volume and are purged as per the retention policy.

To use this option, you should first add following registry key:
<\Registry key needs to be added>


Follow these steps to migrate data source from one volume to the other volume:

1. In the DPM Administrator Console, click **Protection**.

2. In the **Protection** workspace, select the datasource you want to migrate.

    ![Select target workload](Image to be inserted)

3. Click **Move Disk Storage**.

   ![Move disk storage](Image to be inserted)

4. Select the *target disk storage* that you want to migrate to and click **OK**.

   ![Select target disk storage](Image to be inserted)

   This begins the migration process. For monitoring scheduled jobs, you can open another DPM console in parallel, while the migration is in progress.
