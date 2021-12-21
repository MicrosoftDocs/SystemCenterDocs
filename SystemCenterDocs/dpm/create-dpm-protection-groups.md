---
description: This article describes what DPM protection groups consist of and why you should use them.
manager: carmonm
ms.topic: article
author: JYOTHIRMAISURI
ms.prod: system-center
ms.date: 11/25/2021
title: Deploy protection groups
ms.technology: data-protection-manager
ms.assetid: 2a4f4ec8-6185-4fe9-8120-e4dc3b6c9409
ms.author: v-jysur
ms.custom: intro-deployment
---

# Deploy protection groups

::: moniker range=">= sc-dpm-1801 <= sc-dpm-1807"

[!INCLUDE [eos-notes-data-protection-manager.md](../includes/eos-notes-data-protection-manager.md)]

::: moniker-end

A System Center Data Protection Manager (DPM) protection group is a collection of data sources such as volumes, shares, or application workloads, which have common backup and restore settings. The protection group settings specify:

-   **Data sources** - The servers, computers, and workloads you want to protect.

-   **Back-up storage** - How the protected data should be backed up in the short-term and long-term.

-   **Recovery points** - The recovery points from which replicated data can be recovered.

-   **Allocated disk space** - The disk space allocated to data from the storage pool.

-   **Initial replication** - How the initial replication of data should be handled, using either over the network or manually offline.

-   **Consistency checks** - How replicated data should be checked for consistency.


The topics in this section provide guidelines for making the decisions involved in creating a protection group.

## Plan protection groups

You need to decide:

-   How to group resources you want to back up into protection groups.

-   How to store the protection group backup data?

-   How much storage space is required to store data for the protection group?

-   How to recover backup data for the protection group?

There are a few common ways to organize your protection groups:

-   **By computer** - All data sources for a computer belong to the same protection group. Organizing by computer provides a single point of adjustment for the computer's performance loads. However, all data sources have the same backup and recovery settings.

-   **By workload** - You separate files and each application data type into different protection groups. Organizing by workload allows you to manage workloads as a group. However, recovering a multi-application server might require multiple tapes from different protection groups.

-   **By RPO/RTO** - Gather data sources with similar Recovery Point Objectives (RPOs) and Recovery Time Objectives (RTOs) in protection groups. You control the RPO by setting the synchronization frequency for the protection group which determines the amount of potential data loss (in time) during unexpected outages. The RTO is the acceptable amount of time that data is unavailable. The storage methods you select for the protection group directly impacts the RTO.

-   **By data characteristics** - For example how often data changes, how rapidly it grows, or its storage requirements.

## Choosing a name for the protection group
When choosing a name for your Protection Group, the name should be meaningful. The name must be unique to the DPM server. The Protection Group name can include any combination of alphanumeric characters and spaces, but it cannot be longer than 64 characters. DPM does not support special characters such as `|`, `/`, `(`, `)`, or `.`.

## Figure out how much storage space you need
When you create a protection group and select disk-based protection, you must allocate space on the storage pool for the replicas and recovery points for each data source that you have selected for membership in the group, and you must allocate space on protected file servers or workstations for the change journal.

To help you figure out storage capacity, use the [Storage Calculator for DPM with Modern Backup Storage](https://www.microsoft.com/download/details.aspx?id=54301)

DPM provides default space allocations for the members of the protection group. The following table shows how DPM calculates the default allocations.

|Component|Default Allocation|Location|
|-------------|----------------------|------------|
|DPM storage|Data source size x (1 + log change x Retention Range in Days x Number of backups per day) x (1.05)<br /><br /> *For SQL Server data*:<br />-   Data source size x (1 + log change x Retention Range in Days x Number of backups per day) x (1.05) + Transaction Logs<br />|DPM storage pool or custom volume|
|DPM Database| 2 GB <br/>(may increase for SharePoint backups) |DPM Server storage |
|Change journal (for file-protection only)|300 MB|Protected volume on the file server or workstation|


-   **Log change** - the change rate on the database or storage group in question. Log change varies, but for the purposes of the default recommendation in DPM, log change is defined as 3%.

-   **Retention range (RR)** - The number of recovery points stored. The DPM default recommendation is five recovery points.


When you create a protection group, in the **Modify Disk Allocation** dialog box, the **Data Size** column for each data source displays a **Calculate** link. For the initial disk allocation, DPM applies the default formulas to the size of the volume on which the data source is located. To apply the formula to the actual size of the selected data source, click the **Calculate** link. DPM will determine the size of the data source and recalculate the disk allocation for the recovery point and replica volumes for that data source. This operation can take several minutes to perform.

Accept the default space allocations unless you are certain that they do not meet your needs. Overriding the default allocations can result in allocation of too little or too much space.

Allocation of too little space for the recovery points can prevent DPM from storing enough recovery points to meet your retention range objectives. Allocation of too much space wastes disk capacity.

After creating a protection group, if you allocated too little space for a data source, increase the allocations for the replica and recovery point volumes for each data source.

If you allocated too much space for the protection group, remove the data source from the protection group and delete the replica, Then, add the data source to the protection group with smaller allocations.

## Set up protection groups
When you set up a protection group here's what you'll need to do:

### Before you start
Some things to note when creating protection groups:

-   If you're backing up to tape and you have only a single stand-alone tape, use a single protection group to minimize the effort to change tapes. Multiple protection groups require a separate tape for each protection group.

-   Data sources on a computer must be protected by the same DPM server. In DPM a data source is a volume, share, database, or storage group that is a member of a protection group.

-   You can include data sources from more than one computer in a protection group.

-   Protection group members cannot be moved between protection groups. If you decide later that a protection group member needs to be in a different protection group, you must remove the member from its protection group and then add it to a different protection group.

-   If the members of a protection group no longer require protection, stop protection of the protection group. When you stop protection, your options are to retain protected data or to delete protected data.

    -   **Retain protected data option**: Retains the replica on disk with associated recovery points and tapes for the specified retention range.

    -   **Delete protected data option**: Deletes the replica on disk and expires data on the tapes.

-   When you select a parent folder or share, its subfolders are automatically selected. You can designate subfolders for exclusion and also exclude file types by extension.

-   Verify that you do not have more than a 100 protectable data sources on a single volume. If you do, distribute your data sources across more volumes if possible.

-   When you select a data source that contains a reparse point, DPM asks whether to include the reparse point target in the protection group. Mount points and junction points are data sources that contain reparse points. If you include the reparse point, it is not replicated; you must manually re-create the reparse point when you recover the data.

Protection groups are created with the Create New Protection Group wizard with the following settings:

-   **Select Group Members**: Specify the machines and sources you want to back up.

    >[!NOTE]
    > Some of the data sources may not be listed while adding them to the protection group, as the list is displayed from the cache. Click **Refresh** to update the data sources list.

-   **Select data protection method** : Specify how you want to handle short and long-term backup. Short-term back up is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short or long-term). As an alternative to long-term backup to the cloud you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

-   **Select short-term goals**: Specify how you want to back up to short-term storage on disk.   In **Retention range** you specify how long you want to keep the data on disk. In Synchronization frequency you specify how often you want to run an incremental backup to disk. If you don't want to set a back up interval you can check Just before  a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

-   **Specify long-term goals**: Indicate how long you want to keep tape data (1-99 years). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    -   When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    -   When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    You'll also need to specify the tape device/library you want to use, and  whether data should be compressed and encrypted on tape.

-   **Review disk allocation**: You review the storage pool disk space allocated for the protection group. DPM provides a recommended size. You can select to **Automatically grow the volumes** to automatically increase size when more disk space is required for backup.

-   **Choose replica creation method**: Specify how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

-   In **Choose consistency check options**:  Select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time.

-   **Specify online protection data**: If you want to back up to the cloud with Azure Backup, specify the workloads you want to back up.

-   **Specify online backup schedule** : If you're backing up to Azure specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

-   **Specify online retention policy**: If you're backing up to Azure you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

-   **Choose online replication**: If you're backing up to Azure specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](/azure/backup/backup-azure-backup-import-export).


## Initial replication options
When you create a protection group, you must choose a method for creating the initial replica, which copies all the data selected for protection to the DPM server and then runs synchronization with consistency check for each of the replicas.

### Initial replication over the network
DPM can create the replicas automatically over the network, or you can create the replicas manually by restoring the data from removable media such as tape. Automatic replica creation is easier, but, depending on the size of the protected data and the speed of the network, manual replica creation can be faster.

To help you choose a replica creation method, the following table provides estimates for how long DPM takes to create a replica automatically over the network given different protected data sizes and network speeds. The estimates assume that the network is running at full speed and that other workloads are not competing for bandwidth. Times are shown in hours.

**Hours to Complete Automatic Replica Creation at Different Network Speeds**

|Size of Protected Data|512 Kbps|2 Mbps|8 Mbps|32 Mbps|100 Mbps|
|--------------------------|------------|----------|----------|-----------|------------|
|1 GB|6|1.5|< 1|< 1|< 1|
|50 GB|284|71|18|5|1.5|
|200 GB|1137|284|71|18|6|
|500 GB|2844|711|178|45|15|

### Offline replication for Azure Backup
When you're backing up data from the DPM server to Azure you can do the initial replication over the network or using offline seeding. [Read more](/azure/backup/backup-azure-backup-import-export).

### Initial replication manually
If you are deploying DPM to protect data over a WAN and your protection group includes more than 5 GB of data, we recommend that you choose the manual method for creating the replicas.

If you choose manual replica creation, DPM specifies the precise locations on the DPM server where you must create the replicas. Typically, you create the replicas by restoring your most recent backup of the data source from removable media such as tape. After you restore the data, you complete the process by running synchronization with consistency check for each of the replicas.

It is crucial that when you restore the data to the DPM server to create the replica, you retain the original directory structure and properties of the data source, such as time stamps and security permissions. The more discrepancies that exist between the replicas and the protected data source, the longer the consistency checking part of the process takes. If you do not preserve the original directory structure and properties, manual replica creation can take as long as automatic replica creation.

## Naming a Protection Group

When you name the protection group, provide a unique, meaningful name for the group. The name can include any combination of alphanumeric characters and can include spaces, but cannot exceed 64 characters.
