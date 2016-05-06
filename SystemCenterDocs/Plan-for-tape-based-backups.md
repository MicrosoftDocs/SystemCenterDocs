---
title: Plan for tape-based backups
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57b9fed6-9a9b-4c16-b41b-77c5a2a74416
---
# Plan for tape-based backups
Tapes are usually used for long\-term storage of data protected by DPM so that data from protected resources is backed up to disk in the short\-term and then to tape. You can also select to use tape for short\-term protection so that data from protected resources is backed up directly to tape. Note the following:

-   Long\-term storage to tape:

    -   All DPM data can be  backed up to tape for long\-term storage

    -   For long\-term protection to tape full backups are always run.

    -   If you’re using tape for both long\-term and short\-term protection, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] creates copies of the latest short\-term full backup in order to generate the long\-term tape backup. We recommend that you schedule the short\-term protection backup to run a day before the long\-term backup. That way you can be sure you’re using the latest short\-term backup in order to create the long\-term backup.

    -   If you’re using disk for short\-term back up and tape for long\-term, the long\-term backup will be taken from the disk replica.

-   Short\-term storage to tape:

    -   DPM doesn’t support short\-term backup to tape for application data or client computers. Only file data \(volumes, shares, folders\) can be configured for short\-term backup to tape.

    -   For short\-term protection to tape you can use a full backup or a full\/incremental backup \(when backups are set to **Daily**\).

    -   If you don’t have a tape or tape library attached to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server you’ll only be able to select **Disk** for short\-term protection.

-   Note the following for freeing up tapes:.

    -   You can’t free up or erase a tape that contains valid recovery points from any data source. To free up a tape you must removes the sources from the protection group and expiry recovery points on the tape, or modify the protection group settings to clear tape protection.

    -   To restore data from an expired tape you’ll need to mark the tape as free and then unmark it, and then recatalog the tape.

## Tape requirements

-   DPM can backup to tape libraries or standalone tape drives.

-   The tape library or standalone tape must be attached to the DPM server with storage area network \(SAN\) or SCSI.

-   The tape capacity you need will depend on the size of the protected data and the number of tape backup jobs you’ll need to run. To plan for the number of tapes required for a protection group, multiply the required backup frequency by the retention range \(specifies from how far back data can be recovered\).

-   For a list of compatible tape libraries, see [Compatible Tape Libraries for System Center 2012 DPM](http://social.technet.microsoft.com/wiki/contents/articles/17105.compatible-tape-libraries-for-system-center-2012-dpm.aspx) in the TechNet wiki.

-   For standalone tape drives, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] does the following for each protection group:

    -   Appends all short\-term backups to a single tape.

    -   Appends all long\-term backups to a single tape that is different from the short\-term backup tape.

    -   When a tape fills up, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] raises an alert to add a new free tape.

-   For tape libraries note the following:

    -   [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] can allocate two or more tapes for each protection group. All the data sources in a protection group will always append to the same tape for both short\-term and long\-term protection.

    -   If the protection group settings specify the allocation of more than one drive the data sources will be split across tape. For example, if there are five data sources and a drive with a maximum limit of two sources, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] might write three data sources on one tape and two on another. This might cause an uneven distribution of data among tapes, depending the data size, any other scheduled backup tape jobs, and the number of tape drives available at the time.

## Long\-term storage and allocation

-   Long\-term backups to tape allocate a tape for each full backup job, so that each long\-term backup recovery point is always on a new tape.

-   Available free tapes are decremented as tapes are allocated to long\-term or short\-term backup. If no new tape is available for a long\-term backup an alert is issued.

## Short\-term storage and allocation

-   If short\-term backups are configured to use tape and the full backup option is used, each full backup job will require a new free tape.

-   If short\-term backups are configured to use tape and the full\/incremental option is used, the full backups will require a new free tape, and the incremental backups will be appended to a single separate tape.

    Example: If a full backup to tape is scheduled weekly and incremental backups to tape are scheduled daily, then the first full backup will go to a new free tape and all subsequent incremental backups will be appended to another new free tape. If a full backup job fails before it completes, all subsequent incremental jobs will use the existing tape that has valid previous incremental backups.

-   If you trigger two different “create recovery point \(tape\)” actions for two protection group members, DPM create two tape backup jobs, and two tapes will be required. If you trigger a single “create recovery point \(tape\)” action for two protection group members, a single tape it used. This ensures that data for selected protection group members is collocated for ad\-hoc backups to the same tape.

The following table shows how the backup mode influences the number of tapes required for short\-term protection.

|||
|-|-|
|**Backup mode**|**Tapes required**|
|Short\-term tape "full" backup|You’ll need a free tape for each full backup job.|
|Short\-term tape "full and incremental" backup|You’ll need a free tape for each scheduled full backup job. The incremental backup will be appended to a single separate tape.<br /><br />For example, if a full backup is scheduled weekly and incremental backups are scheduled daily, then the first full backup will go to a new free tape and all subsequent incremental backups for six days will be appended to another new free tape.<br /><br />As tapes fill up, new free tapes are allocated.|
|Long\-term|You’ll need a free tape for each full backup job. If you’re storing tapes offsite, this ensures that each long\-term backup recovery point is on a new tape.|

