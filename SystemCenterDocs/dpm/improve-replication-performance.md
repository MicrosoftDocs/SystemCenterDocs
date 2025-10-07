---
description: This article describes the steps you can take to improve replication performance in DPM.
ms.topic: how-to
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: Improve replication performance
ms.subservice: data-protection-manager
ms.assetid: dc7b7b49-dcbb-4e44-9ea7-31374c5773ff
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: UpdateFrequency2, engagement-fy24
---

# Improve replication performance

There are many steps you can take to optimize the performance of System Center - Data Protection Manager (DPM) data replication and synchronization, including network throttling, data compression, staggering synchronization, and optimizing express backups.

## Network throttling

Network bandwidth usage throttling is configured at backed up machine level and you  can specify different network bandwidth usage throttling rates for work hours, non-work hours, and weekends, and you define the times for each of those categories. Enable throttling as follows:

1. Open DPM console > **Management** > **Agent**, select the machine on which you want to throttle bandwidth > **Throttle**.

2. Select **Throttle** > **Enable network bandwidth usage**.

3. Select **Throttle Settings** and **Work Schedule** for the machine and select **OK**.

    >[!NOTE]
    >You can configure network bandwidth usage throttling separately for work hours and nonwork hours, and you can define the work hours for the protected computer.

4. To apply your settings, select **OK**.

> [!NOTE]
> Network bandwidth usage can be also limited by Group Policy.

The Group Policy reservable bandwidth limit on the local computer determines the combined reservable bandwidth for all programs that use the Packet Scheduler, including DPM. The DPM network bandwidth usage limit determines the amount of network bandwidth that DPM can consume during replica creation, synchronization, and consistency checks.

If the DPM bandwidth usage limit, either by itself or in combination with the limits of other programs, exceeds the Group Policy reservable bandwidth limit, the DPM bandwidth usage limit might not be applied.
For example, if a DPM computer with a 1 gigabit per second (Gbps) network connection has a Group Policy reservable bandwidth limit of 20%, 200 Mbps of bandwidth is reserved for all programs that use the Packet Scheduler. If DPM bandwidth usage is then set to a maximum of 150 Mbps while Internet Information Services (IIS) bandwidth usage is set to a maximum of 100 Mbps, the combined bandwidth usage limits of DPM and IIS exceed the Group Policy reservable bandwidth limit and the DPM limit might not be applied. To resolve this issue, reduce the DPM setting for network bandwidth usage throttling.

## Enable data compression

On-the-wire compression is configured at the protection-group level for backup to tape. Compressing data reduces the space needed on the tape and increases the number of backup jobs that can be stored on the same tape. Compression doesn't significantly increase the time required to complete the backup job. Encryption increases data security and also doesn't significantly increase the time required for the backup job. Encryption requires a valid certificate on the DPM server. Configure compression as follows:

1. Open the DPM Administrator console > **Protection** view.

2. Select **Optimize performance**.
   On the **Network** tab, check **Enable on-the-wire compression**.

## Stagger synchronization start times

To optimize performance, you can offset the start time of synchronization jobs across different protection groups so that all of them don't start at the same time. Offsetting synchronization start times can also be used to optimize secondary protection of another DPM server. Offset as follows:

1. Select DPM Administrator Console > Protection and select a protection group.

2. Select **Optimize performance**. On the Network tab, select the hours and minutes to offset the start of the synchronization job in the **Offset** \<time\> start time by field.

## Optimize express backups

To provide quick recovery of application data, DPM must create an express full backup periodically. The express full backup operation typically increases the demand on the server's resources by 5% for several minutes. To reduce the demand on the server's resources, you can schedule fewer express full backups, but this can increase the data recovery time. Modify the schedule as follows:

1. Select  DPM Administrator Console > **Protection** and select the  protection group for which you want to modify the express full backup schedule.

2. Select **Optimize performance** and on the **Express Full Backup** tab, select the available times for the express full backups and select **Add**.
   Select the days of the week for the express full backups.

## Optimize client computer performance

On some client computers, you may notice the computer running slow when a backup is in progress. You can improve the client computer’s responsiveness by adding the following registry setting.
The *ClientProtection* key and *WaitInMSPerRequestForClientRead* value aren't present by default, you must create them.

- **Key**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Agent\ClientProtection`
- **Value**: `WaitInMSPerRequestForClientRead`
- **Data**: 50
- **Type**: DWORD

The default value for this DWORD is 50 (32H) and the supported range is 40 to 100. You can increase it to 75 to improve client responsiveness. If you want to increase/improve backup speed at the expense of responsiveness, reduce the value to 40.

>[!NOTE]
> Increase in `WaitInMSPerRequestForClientRead` value causes the DPM synchronization jobs to take longer.
