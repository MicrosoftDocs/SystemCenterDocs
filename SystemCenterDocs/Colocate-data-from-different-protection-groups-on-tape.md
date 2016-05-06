---
title: Colocate data from different protection groups on tape
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88d7ace9-91a7-450d-9054-ee0b85bf3969
---
# Colocate data from different protection groups on tape
System Center Data Protection Manager \(DPM\) allows you to colocate data from different protection groups on a tape. This allows you to group recovery points of multiple protection groups on a single tape, and optimizes tape usage if you have many small protection groups. Note the following:

1.  DPM 2010 required you to run a Windows PowerShell command to enable colocation on tape. This is no longer required for DPM 2012.

2.  Encrypted and non\-encrypted datasets cannot be co\-located on the same tape.

3.  Datasets from short\-term backup to tape and long\-term backup to tape cannot be colocated.

4.  When tape co\-location is enabled, a tape on to which offsite backup is written will not be shown as **Offsite Ready** unless one of the following conditions are met:

    -   The tape is full.

    -   One of the datasets has expired.

    -   Write\-period ratio has been crossed. \(By default, this is first backup time \+ 15 per cent of retention range.\)

## Set up tape colocation and optimization
To optimize tape usage, [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] uses protection group sets. A protection group set is a set of protection groups for which the backups will be colocated on tape. You use the tape optimization feature in [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] to allow multiple protection groups to share a tape to store their backups. Note the following:

-   Data from a protection group that belongs to a set will not necessarily be colocated to a tape. Colocation will be decided by the rite period and expiration tolerance values.

-   The write period is the length of time for which a tape is available for writing new backups. The tape is marked as Offsite Ready after this.

-   The expiration tolerance is the maximum length of time for which an expired recovery point can remain on a tape until the tape is marked as expired.

Use the following procedures to set up tape optimization.

### Create a protection group

1.  Go to the Library view.

2.  Click **Optimize usage** on the **Actions** pane.

    This brings up the Tape Optimization Setup dialog box.

    You can use this screen to create, modify or delete protection group sets.

### Create a protection group set

1.  Click **Create** on the Tape Optimization Setup dialog box.

2.  Enter a unique name to identify the protection group set.

3.  Select the protection groups to add to the protection group set.

4.  If you do not want protection groups with different retention periods to use the same tape, select **Don’t allow backups of different retention periods to co\-locate on the same tape**.

5.  Click **Advanced** to set Write Period and Expiry Tolerance values.

After creating a protection group set you can modify its values by clicking **Modify** on the Tape Optimization Setup dialog box. Values you can modify include the following: set name, the protection groups that belong to the set, and allowing backups of different retention periods to collocate on the same tape.

-   Name of the protection group set

-   The protection groups that belong to the set

-   Allow backups of different retention periods to be collocate on the same tape.

-   Name of the protection group set

-   The write period

-   Expiry tolerance values

### Set the write period and expiry tolerance
The following example scenarios illustrate how to set the write period and expiry tolerance.

### Example: Scenario 1

|Scenario conditions|Scenario policy \(set by administrator\)|Scenario tape usage|
|-----------------------|--------------------------------------------|-----------------------|
|-   For a given retention range, all backups happen on the same day across the protection groups.<br />-   Tapes are taken out of the library every week.<br />-   Month retention tapes are sent to one physical vault and year retention tapes are taken to another.<br />-   Corporate policy dictates that tapes cannot contain expired datasets \(Zero tolerance policy\).|-   Do not co\-locate different retention ranges to the same tape.<br />-   Write period should be 1. That is, a tape can be written to only on the day of the first backup to that tape.<br />-   Expiry tolerance is 0|-   Every day at least one tape will be offsite\-ready. The daily backups of protection groups 1, 2, and 3 will be co\-located. This tape will expire at midnight of the eighth day.<br />-   Every Monday, all the weekly backups of protection groups 1, 2, and 3 will be co\-located. These tapes will be offsite\-ready after the last backup is written, and will expire a month later.<br />-   On the first day of every month, all the monthly backups of protection groups 1 and 2 will be co\-located. These tapes will be offsite\-ready after the last backup is written, and will expire a year later.|

This policy results in the following settings.

|Protection Groups|Frequency|Retention|Occurs on|
|---------------------|-------------|-------------|-------------|
|1,2,3|1 day|1 week|Daily|
|1,2,3|1 week|1 month|Every Monday|
|1,2|1 month|1 year|First of every month|

### Example: Scenario 2

|Scenario conditions|Scenario policy \(set by administrator\)|Scenario tape usage|
|-----------------------|--------------------------------------------|-----------------------|
|-   For a given retention range \(except a week’s retention\), backups are staggered across days across the protection groups.<br />-   Tapes are taken out of the library every week.<br />-   Month retention tapes are sent to one physical vault and yearly retention tapes are sent to another.<br />-   Corporate policy dictates that tape may contain expired datasets, but for not more than a week \(low tolerance policy\).|-   Do not co\-locate different retention ranges to the same tape.<br />-   Write period is six days. That is, a tape can be written to until six days after the first backup day.<br />-   Expiry tolerance is six days.|-   Every week at least one tape will be offsite\-ready. The daily backups of protection groups 1, 2, and 3 will be co\-located on it. This tape will expire at midnight of the fifteenth day..<br />-   Every Monday, Wednesday, and Friday, weekly backups of protection groups 1, 2, and 3 will be co\-located. These tapes will be offsite\-ready on the Sunday of the week, and will expire a month later|

This policy results in the following settings.

|Protection Groups|Frequency|Retention|Occurs on|
|---------------------|-------------|-------------|-------------|
|1|1 day|1 week|Every day|
||1 week|1 month|Monday|
||1 month|1 year|First of every month|
|2|1 day|1 week|Every day|
||1 week|1 month|Wednesday|
||1 month|1 year|Second of every month|
|3|1 day|1 week|Every day|
||1 week|1 month|Friday|
||1 month|1 year|NA|

### Example: Scenario 3

|Scenario conditions|Scenario policy \(set by administrator\)|Scenario tape usage|
|-----------------------|--------------------------------------------|-----------------------|
|-   For a given retention range, all backups happen on the same day across the protection groups.<br />-   1\-year retention backups are sent outside the library. There is no need to co\-locate them.<br />-   Expired datasets may remain on tapes for up to a month \(medium tolerance policy\).|-   Allow the co\-location of different retention ranges to the same tape.<br />-   Write period is 13 days. That is, a tape can be written to until 13 days after the first backup day.<br />-   Expiry tolerance is one month.|-   Every second week, at least one tape will be offsite\-ready. The weekly backups of protection groups 1 and 2 will be co\-located on it.<br />-   This tape may also have one monthly backup of each protection group.|

This policy results in the following settings.

|Protection Groups|Frequency|Retention|Occurs on|
|---------------------|-------------|-------------|-------------|
|1,2|1 week|2 weeks|Every Saturday|
|1,2,3|1 month|1 month|Second of every month|
|1,2,3|1 month|1 year|First of every month|


