---
title: Back up protected data_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a2d55059-045d-4f61-b154-425047949b4a
---
# Back up protected data_1
DPM backs up the data sources it protects. You can backup long\-term data to tape, and short\-term data to disk, disk and Microsoft Azure, or less commonly to tape. Read about DPM backup types in [Data Protection](assetId:///163f7ad3-69b4-4245-aa33-fc14d3ca509f), and backup storage options in [Backup and synchronization overview](assetId:///9e38d9e8-68f1-46bb-93ea-94e1d584abd6).

DPM provides scheduled and on\-demand backups for protected data.

-   **Scheduled backups**: In DPM you configure backups for a specific protection group. You configure and schedule backups as follows:

    -   **Short\-term**—You schedule a start time for backups that replicate to short\-term storage.

    -   **Long\-term**—You schedule settings and a start time for backups that replicate to long\-term storage

    -   **Backup windows**—By default in DPM you schedule the start time for backup of a protection group but you don’t specify an end time. From DPM 201 R2 Update 3 onwards you can configure backup windows that specify when a backup job should begin and end. This feature allows you granular control for scaling by creating backup windows outside of production hours. Note that this is currently only supported for virtual machines. Backup windows for other kinds of workloads in protection groups aren’t supported.

-   On\-demand backups—You can run an on\-demand backup for specific data sources in a protection group. Note that if you want to run a single scheduled backup you’ll need to create a new protection group to do that.

[Configure and run backups](./Configure-and-run-backups.md)

[Run system state and bare metal backups](./Run-system-state-and-bare-metal-backups.md)


