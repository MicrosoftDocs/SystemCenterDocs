---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Prepare data storage
ms.technology:  data-protection-manager
ms.assetid:  ebe047b4-0737-4ce5-8fe2-d5e0cfd9b852
---

# Prepare data storage

>Applies To: System Center 2016 Technical Preview - Data Protection Manager

A major part of your DPM deployment will be figuring out how to store data backed up by DPM. Learn about:

-   [Short and long-term storage](#BKMK_Storage)

-   [Cloud storage with Azure Backup](#BKMK_Azure)

-   [Disk storage](#BKMK_Disk)

-   [Tape storage](#BKMK_Tape)

## <a name="BKMK_Storage"></a>Short and long-term storage overview
In DPM you'll need to select short and long-term storage for backed up data.

|Storage|Short-term|Long-term|Characteristics|
|-----------|---------------|--------------|-------------------|
|Azure cloud|Suitable for short-term storage|Suitable for long-term storage up to 3360 days|-   Efficient and cost-effective offsite storage solution for short and long-term storage.<br />-   Azure can be used as storage for Hyper-V, SQL Server, and file server data. Azure can only be used to backup data from servers running Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 with SP1.<br />-   DPM must be running on System Center 2012 SP1 or later to use Azure Backup.|
|Tape|Some workloads can be backed up directly to tape (D2T) for short-term storage.<br /><br />These include file data (volumes, shares, folders), system state, SQL Server, Hyper-V, and Exchange databases not configured on a DAG.|All workloads can be backed up to tape for long-term offsite storage (D2D2T)|-   Short-term backup to tape might be useful for data that doesn't change often and thus doesn't require frequent backup.<br />-   Long-term offsite tape storage is useful for data which must be kept in order to fulfil statutory obligations<br />-   When backing up to tape DPM only supports incremental backup to tape for file data (volumes, shares, folders). Backing up workload data to tape runs a full backup.<br />-   If you're using tape for both long-term and short-term protection, DPM creates copies of the latest short-term full backup in order to generate the long-term tape backup. We recommend that you schedule the short-term protection backup to run a day before the long-term backup. That way you can be sure you're using the latest short-term backup in order to create the long-term backup.<br />-   If you're using disk for short-term back up and tape for long-term, the long-term backup will be taken from the disk replica.<br />-   Data recovery from tape might be slow, and thus better suited to data with a high recovery point objective (RPO) that doesn't need to accessed and recovered within a short critical period after failure.<br />-   You can't free up or erase a tape that contains valid recovery points. You'll need to remove the sources from a protection group and expire the recovery points, or modify the protection group settings to clear tape protection. To expiry a tape you mark it as free and then unmark it and recatalog.<br />-   Tape backup and recovery might require manual intervention such as tape rotations.<br />-   Long-term storage capacity can be increased by adding more tapes.<br />-   A tape library or standalone tape drive must be physically attached to the DPM server. The tape library can be direct SCSI attached or SAN.|
|Disk|All data backed up to DPM can be stored on disk for short-term storage (D2D)|No long term storage to disk.|-   Disks provide a quick method of data backup and recovery. It's useful for data that has a low RPO and thus needs to be recovered quickly after failure.<br />-   Disks can provide redundancy using disk technologies such as RAID.<br />-   Maximum disk retention is 448 days.<br />-   Disk backup has no impact on running workloads.|

## <a name="BKMK_Azure"></a>Prepare cloud storage (Azure Backup)
You can back up protected DPM data to Azure using the Azure Backup service. This is useful in a couple of scenarios:

-   **DPM is deployed on-premises as a physical server or virtual machine**—If you deploy DPM as a physical server or as an on-premises Hyper-V virtual machine you can back up data with Azure Backup in addition to backing data up to disk and tape.

-   **DPM is deployed as a virtual machine in Azure**—If DPM is deployed as an Azure virtual machine (possible from System Center 2012 R2 with Update 3) you can back up data to Azure disks attached to the DPM Azure virtual machine and then offload data storage with backup to Azure Backup.

When you set up a protection group in DPM you select disk for short-term storage and then you enable online backup to Azure.  Note that:

-   There are a number of prerequisites and limitations.[Read more](https://azure.microsoft.com/en-us/documentation/articles/backup-azure-dpm-introduction/#requirements-and-limitations).

-   You'll need to set up Azure Backup before you enable backup to the cloud for a protection group in the DPM console. [Learn](https://azure.microsoft.com/en-us/documentation/articles/backup-azure-dpm-introduction/) how to set up Azure Backup with DPM.

-   When you back up a protection group to Azure you can retain data for up to 3360 days. In Azure Backup each backup is stored as a recovery point. The maximum amount of recovery points is 120 for daily synchronization, but you can create a less granular backup policy.

    |Synchronize every x weeks|Maximum retention algorithm|Maximum retention (days)|
    |-----------------------------|-------------------------------|------------------------------|
    |1|120 x7 x 1|840|
    |2|120 x 7 x 2|1680|
    |3|120 x 7 x 3|2520|
    |4|120 x 7 x 4|3360|

## <a name="BKMK_Disk"></a>Prepare disk storage
DPM backs up data to disk for short-term storage by saving data to the DPM storage pool. The storage pool is the set of disk on which the DPM  server stores the replicas and recovery points for the protected data. Before you can store data on disk you'll need at least one disk in a storage pools. You can use any of the following for the storage pool:

-   Direct attached storage (DAS)

-   Fiber Channel storage area network (SAN)

-   iSCSI storage device or SAN

## Best practices for the storage pool

|Best practice|Details|
|-----------------|-----------|
|Disk limitations|-   The DPM server needs at least two disks installed. A dedicated disk for the startup, system, and DPM installation files; and one dedicated to the storage pool. In DPM a disk is defined as any disk device manifested as a disk in the Windows Disk Management tool. DPM does not add any disk containing startup files, system files, or any component of the DPM installation to the storage pool.<br />-   Disks added to the storage pool shouldn't partitions. To prepare disks, DPM reformats them and erases any data<br />-   The storage pool supports most disk types, including IDE,  SATA and SCSI, and it supports both the master boot record (MBR) and GUID partition table (GPT) partition styles. We strongly recommend that you use GPT disks.<br />-   If you use a SAN for the storage pool, we recommend you create a separate zone for the disk and tape. Don't mix the devices in a single zone.<br />-   DPM doesn't support USB/1394 disks in the  storage pool.<br />-   You can't use Storage Spaces for the disk storage pool.<br />-   Some original equipment manufacturers (OEMs) include a diagnostic partition that is installed from media that they provide. The diagnostic partition might also be named the OEM partition, or the EISA partition. EISA partitions must be removed from disks before you can add the disk to the storage pool.<br />-   You can substitute custom volumes that you define in Disk Management for volumes in the storage pool.<br />-   We recommend you use esxtensible hardware so you can add more capacity if you need to.|
|Dedup support|DPM running as a Hyper-V virtual machine can store backup data to VHDs in shared folders on a Windows File Server with data deduplication enabled. For more information, see [Deduplicate DPM storage](../Deploy/Deduplicate-DPM-storage.md).|
|Capacity requirements|Capacity requirements depend primarily on the size of protected data, the daily recovery point size, expected volume data growth rate, and retention range objectives.<br /><br />Daily recovery point size refers to the total size of changes made to protected data during a single day. It is roughly equivalent to the size of an incremental backup. Retention range refers to the number of days for which you want to store recovery points of protected data on disk. For files, DPM can store a maximum of 64 recovery points for each volume included in a protection group, and it can create a maximum of 8 scheduled recovery points for each protection group each day.<br /><br />Retention range is the number of days you want to store recovery points of protected data on disk. For files, DPM can store a maximum of 64 recovery points for each volume included in a protection group, and it can create a maximum of 8 scheduled recovery points for each protection group each day. The limit of 64 recovery points for files is a Volume Shadow Copy Service (VSS) limitation. The recovery point limit doesn't apply to application data.<br /><br />We recommend you make the storage pool twice size of the protected data. This assumes a daily recovery point size that's 10% of the protected data size and a 10 days retention range. To get a good estimate of size, review an incremental backup for an average day. For example, if the incremental backup for 100 GB of data includes 10 GB of data, your daily recovery point size will probably be around 10 GB. Obviously you'll need to adjust for the 10% and 10 day estimation doesn't work for your organization.<br /><br />Note that the longer your retention range, the fewer recovery points you can create each day. For example, if your retention range objective is 64 days, you can create just one recovery point each day. If it's 8 days you can create 8 recovery points each day. With a retention range objective of 10 days, you can create approximately 6 recovery points a day.|
|Disk configuration|If you're using direct-attached storage for the  storage pool, you can use any hardware-based configuration of redundant array of independent disks (RAID), or you can use a "just a bunch of disks" (JBOD) configuration. Don't create a software-based RAID configuration on disks that you will add to the storage pool.<br /><br />To decide on disk configuration, consider the relative importance of capacity, cost, reliability, and performance in your environment. For example, because JBOD doesn't consume disk space for storing parity data, it'll make maximum use of storage capacity. For the same reason, the reliability of JBOD configurations is poor; a single disk failure inevitably results in data loss.<br /><br />For a typical deployment, DPM recommends a RAID 5 configuration, which offers an effective compromise between capacity, cost, reliability, and performance.<br /><br />To help you evaluate options for configuring the disks in your storage pool, the table below compares the trade-offs between JBOD and the various levels of RAID, on a scale from 4 (very good) to 1 (acceptable).|
|Custom values|In some cases you might want to use a custom volume, where a custom volume isn't in the storage pool and is used to store the replica and recovery points for a protection group member. For example you might want a greater amount of control over storage for specific data sources or critical data needs to be stored using a high-performance LUN on a SAN.<br /><br />Any volume that's attached to the DPM server can be selected as a custom volume, except the volume that contains the system and program files. To use custom volumes for a protection group member, two custom volumes must be available: one volume to store the replica and one volume to store the recovery points.<br /><br />DPM can't manage the space in custom volumes. If DPM alerts you that a custom replica volume or recovery point volume is running out of space, you'll need to manually change the size of the custom volume by using Disk Management.<br /><br />You can't change the selection of storage pool or custom volume for a protection group member after the group is created. To do this you'll need to stop protecting the data source and then add it again to a protection group.|

### Compare disk options
**Disk**

|Disk Configuration|Capacity|Cost|Reliability|Performance/scalability|
|----------------------|------------|--------|---------------|----------------------------|
|JBOD|4|4|1|4|
|RAID 0|4|4|1|4|
|RAID 1|1|1|4|3|
|RAID 5|3|3|3|3|
|RAID 10|1|1|4|4|

### Configure the storage pool
After you have at least one disk set up in accordance with the prerequisites, you can add it to the storage pool.

-   In DPM Administrator Console, click **Management** > **Disks**.

-   Click **Add** on the tool ribbon, and in **Add Disks to Storage Pool** select the disk you want to add form the **Available disks** list.

After the storage pool is set up, when you create protection groups that include data sources you want to back up, you'll be able to configure disk as short-term storage for that backed up data.

## <a name="BKMK_Tape"></a>Prepare tape backup

-   DPM can backup to tape libraries or standalone tape drives.

-   You'll need to attach your tape libraries or standalone tape drives to the DPM server with SAN or SCSI. Tape devices must be compatible with DPM. Read about [Identify compatible tape libraries](Identify-compatible-tape-libraries.md) .

-   Get a list of [Compatible Tape Libraries](http://social.technet.microsoft.com/wiki/contents/articles/17105.compatible-tape-libraries-for-system-center-2012-dpm.aspx).

-   The tape capacity you need depends on the size of the protected data and the number of tape backup jobs you'll run. To plan for the number of tapes required for a protection group, multiply the required backup frequency by the retention range.

-   For standalone tape drives, DPM does the following for each protection group:

    -   Appends all short-term backups to a single tape.

    -   Appends all long-term backups to a single tape that is different from the short-term backup tape.

    -   When a tape fills up, DPM raises an alert to add a new free tape.

-   For tape libraries:

    -   DPM can allocate two or more tapes for each protection group. All the data sources in a protection group will always append to the same tape for both short-term and long-term protection.

    -   If the protection group settings specify the allocation of more than one drive the data sources will be split across tape. For example, if there are five data sources and a drive with a maximum limit of two sources, DPM might write three data sources on one tape and two on another. This might cause an uneven distribution of data among tapes, depending the data size, any other scheduled backup tape jobs, and the number of tape drives available at the time.

-   Long-term backups to tape allocate a tape for each full backup job, so that each long-term backup recovery point is always on a new tape.

-   Available free tapes are decremented as tapes are allocated to long-term or short-term backup. If no new tape is available for a long-term backup an alert is issued.

-   If short-term backups are configured to use tape and the full backup option is used, each full backup job will require a new free tape.

-   If short-term backups are configured to use tape and the full/incremental option is used, the full backups will require a new free tape, and the incremental backups will be appended to a single separate tape.

    Example: If a full backup to tape is scheduled weekly and incremental backups to tape are scheduled daily, then the first full backup will go to a new free tape and all subsequent incremental backups will be appended to another new free tape. If a full backup job fails before it completes, all subsequent incremental jobs will use the existing tape that has valid previous incremental backups.

-   If you trigger two different "create recovery point (tape)" actions for two protection group members, DPM create two tape backup jobs, and two tapes will be required. If you trigger a single "create recovery point (tape)" action for two protection group members, a single tape it used. This ensures that data for selected protection group members is collocated for ad-hoc backups to the same tape.

#### Install and configure tape devices

1.  Attach tape drive—Follow the instructions provided with the tape device to attach and install it on the DPM server.

2.  Verify serial numbers—Check that the medium changer and tape drives have serial numbers. DPM uses these for identification. Installed tape devices are listed in Device Manager.

3.  Add firewall exceptions—Add firewall exceptions so that DPM can detect the tape:
    C:\Program Files\Microsoft System Center 2012\DPM\SQL\SSQL10_50.MSDPMV4RC\MSSQL\Binn\sqlservr.exe
    C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe
    C:\Program Files\Microsoft System Center 2012\DPM\DPM\bin\DPMLA.exe

4.  Add firewall exceptions—Add firewall exceptions so that DPM can detect the tape:
    C:\Program Files\Microsoft System Center 2012\DPM\SQL\SSQL10_50.MSDPMV4RC\MSSQL\Binn\sqlservr.exe
    C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe
    C:\Program Files\Microsoft System Center 2012\DPM\DPM\bin\DPMLA.exe

5.  Detect manually—DPM automatically detects tape devices that are physically attached to it and they're displayed in the Libraries workspace of the Management view. If a device isn't displayed, you can detect it manually with the Rescan button. This might take a few minutes. After you rescan, check that the details displayed in Device Manager and in the tape library are the same

6.  Set up tape sharing—Set up tape sharing if you want to share a single tape library across multiple DPM server. Note that:

    -   The tape library is typically a collection of tape drives that automatically mount and dismount tape media.

    -   The tape library must be in a storage area network (SAN) environment.

7.  The library server is a computer on which DPM is installed, the library-sharing command has been run, and the medium changer is enabled.
     A library client is a computer on which DPM is installed, the library-sharing command has been run, and the medium changer is not enabled.
    We recommend that the system configuration of the library server computer and all library client computers be as similar as possible, and that you do not configure any protection groups on the library server.

8.  All DPM servers using a shared library must use a similar SQL Server setup for hosting DPM databases. For example, they should all use a local instance of the DPM database or all of them should use a remote instance. You cannot have some DPM servers using local instance and others using a remote instance.

After you've set up tapes, when you create a protection group including data sources you want to protect, you'll be able to select tape for long-term and short-term data storage.

If you want to use a shared library for multiple DPM servers continue to the next procedure.

#### Set up tape sharing

1.  On the computer that will be the library server for the shared library, enable the medium changer by using Device Manager.
    On each library client computer, ensure that the medium changer is not enabled.

2.  Enable the Named Pipes protocol for the SQL Server instances of the library server and library client computers. Then restart the SQL service.

3.  To configure the DPM servers to use a shared library, on each library client computer, open an elevated Command Prompt window, and then run the following commands:

    -   `cd <system drive>:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Setu`p

    -   `AddLibraryServerForDpm.exe -DpmServerWithLibrary <FQDN of library server>` where <FQDN of library server> is the fully qualified domain name of the library server.

4.  On the library server computer, open an elevated Command Prompt window, and then run the following commands one time for each library client. For example, if your library server supports three library clients, you must run this command three times on the library server.

    -   `cd <system drive>:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Setup`

    -   `AddLibraryServerForDpm.exe - ShareLibraryWithDpm <FQDN of library client>` where <FQDN of library client> is the fully qualified domain name of the library client.

5.  On each library client computer (and not on the library server), open an elevated Command Prompt window, and then run the following commands. Before you run the commands, on all library client computers ensure that both the SQL Server (MSDPM2012) and SQL Server Agent (MSDPM2012) services use a domain user account as the logon account, not a local account, which is the default configuration, and that the domain account that is used is a member of the local Administrator group on all of the computers that are sharing the library.

    -   `cd <system drive>:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\Setup`

    -   `SetSharedDpmDatabase -DatabaseName <SqlServer\Instance\DatabaseName> [-DoNotMoveData]` where <SQLServer\Instance\Databasename> is the database name of the library server., You can find the name in the **About DPM** window in the DPM Administrator console. You can copy this information from there, using your mouse

6.  n DPM Administrator Console on the library server, perform a rescan, and then perform a rescan or refresh on each of the library client computers.

    The quickest way to see all media on all of the DPM servers is to perform a rescan on each, followed by a detailed inventory. Next, on any one of the servers, mark a number of media as free, and then perform a refresh on the other servers.
    After you've configured library sharing, you can use the shared tape library as if it were attached to each DPM server.



