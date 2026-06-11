---
description: This article describes how to stop protection for workloads that are already protected by System Center Data Protection Manager
ms.topic: how-to
ms.service: system-center
ms.date: 06/11/2026
title: Stop Protection for Workloads
ms.subservice: data-protection-manager
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.update-cycle: 1095-days
monikerRange: '>sc-dpm-2016'
---

# Stop protection for workloads in DPM administrator console

This article describes how to stop protection for workloads that System Center Data Protection Manager (DPM) is currently protecting. You can stop this protection by using the DPM Administrator Console.

## Prerequisites

Before you stop protection for a workload, ensure that:

- You have access to the DPM Administrator Console with DPM Administrator permissions.
- The workload is currently in an active protection group.

## Stop protection by using DPM Administrator Console

You can stop protection at the Protection Group level. The following steps outline how to stop protection at this level. Alternatively, you can also stop protection for an individual data source by selecting the data source instead of the protection group.

To stop the protection for a workload, follow these steps:

1. On the **DPM Administrator Console**, select **Protection**.

     :::image type="content" source="media/stop-protection/protection-group.png" alt-text="Screenshot of Protection group page.":::

1. On the **Protection** view, locate the protection group (containing the datasource) for which you want to stop protection.

1. To stop protection at the **Protection Group level**, right-click the **Protection group**, and then select **Stop protection of group** that stops protection for all associated datasources.

   If you want to stop protection for an individual datasource, select the specific data source instead of the Protection Group.

     :::image type="content" source="media/stop-protection/stop-protection.png" alt-text="Screenshot of stop protection option.":::

1. On the **Stop Protection** page, choose the appropriate data retention option.
     - **Disk data retention configurations**:

         | **Option** | **Description** |
         |---|---|
         | Retain replicas on disk | Keeps the existing replica data (full copy of protected data) on the DPM storage pool. You can use this data for recovery at a later time. |
         | Delete data source replicas from disk | Permanently removes the replica from the DPM storage pool, freeing up disk space. Recovery from local disk is no longer possible. |

     - **Online data retention configuration**:

         | **Option** | **Description** |
         |---|---|
         | Retain forever | Cloud recovery points are kept indefinitely in the Recovery Services Vault, regardless of any retention policy. Data remains recoverable from Azure at any time. |
         | Retain online recovery points by policy | Cloud recovery points are kept according to the existing retention policy (daily, weekly, monthly, or yearly). Recovery points expire naturally as the policy dictates. |
         | Delete Storage Online | All cloud recovery points are deleted immediately or during the next housekeeping task. No online recovery is possible after deletion. |

     :::image type="content" source="media/stop-protection/retention-data.png" alt-text="Screenshot of Disk and Online retention data.":::

1. Review the selected parameters and select **Stop Protection** to confirm the operation.

     :::image type="content" source="media/stop-protection/review-parameters.png" alt-text="Screenshot of selected parameters.":::

## Verify the stop protection operation

Verify the stop protection operation in the following ways:

- After the successful completion of stop protection operation, a confirmation message appears indicating that protection is stopped.
    
  :::image type="content" source="media/stop-protection/verify-operation.png" alt-text="Screenshot of Stop protection operation completion.":::

- The protection group moves to an Inactive state.
     
  :::image type="content" source="media/stop-protection/inactive-protection.png" alt-text="Screenshot of Inactive protection pane." lightbox="media/stop-protection/inactive-protection.png":::

>[!NOTE]
>If you select the retain option, the existing recovery points remain available for restore operations. Inactive protection groups retain their data based on the retention options you selected. You can resume protection on an inactive protection group later.

## Recovery data after stopping protection

If you retain disk replicas or online recovery points during the stop protection process, the Recovery view of the DPM Administrator Console shows the retained recovery points.

While recovering, select **Disk** or **Online** as the recovery source.

:::image type="content" source="media/stop-protection/recovery-pane.png" alt-text="Screenshot of Recovery pane.":::

If you select **Retain Online recovery points by policy**, the console shows the applicable retention policy and expiry date when you select an online recovery point.

:::image type="content" source="media/stop-protection/recovery-time.png" alt-text="Screenshot of Recovery time.":::

For detailed steps on restoring data from recovery points, refer to your workload-specific article.

## Delete inactive protection data

When you no longer need the retained data for restore, delete the local and online recovery points permanently from the inactive protection group to free disk space and cloud storage.

To delete inactive protection data, follow these steps:

1. In the DPM Administrator Console, select **Protection**.
1. Under **All Protection Groups**, select **Inactive Protection**.
1. Right-click the data source and select **Remove inactive protection**.
      :::image type="content" source="media/stop-protection/remove-inactive-protection.png" alt-text="Screenshot of Remove inactive protection option.":::
1. In the **Delete inactive protection** dialog, select **Delete replica on disk** and **Delete online storage** and then select **OK**.
      :::image type="content" source="media/stop-protection/delete-inactive-protection.png" alt-text="Screenshot of delete inactive protection dialog.":::
The removal task runs and shows a success confirmation.
