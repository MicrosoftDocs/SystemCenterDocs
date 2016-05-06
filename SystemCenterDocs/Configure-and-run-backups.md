---
title: Configure and run backups
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d219997-0877-4444-a800-dfe11be726f8
---
# Configure and run backups
Configure and run scheduled and on\-demand backups.

-   [Configure backups to short\-term storage](#BKMK_Short)

-   [Configure backups to long\-term storage](#BKMK_Long)

-   [Configure backup windows for virtual machines](#BKMK_VM)

-   [Run on\-demand backups](#BKMK_Demand)

## Configure scheduled backups
When you create a protection group or modify its settings, configure backup settings for short\-term and long\-term protection. For virtual machines in protection groups you can refine backup scheduling by specifying start and finish times to create specific time windows in which those backups should run.

When you create a new protection group you specify how the initial replication of data should occur. After this initial replication backups occur in accordance with the settings you’ve specified.

### <a name="BKMK_Short"></a>Configure backups to short\-term storage

|Setting|Short\-term backup to disk \(or disk\+Azure\)|Short\-term backup to tape|
|-----------|-------------------------------------------------|------------------------------|
|Retention range<br /><br />How long data should be kept in short\-term storage|Set from 1\-64 days<br /><br />When you backup to Azure Site Recovery in addition to disk data can be stored in Azure for a maximum of 120 days with a single synchronization per day. You can do up to two synchronizations but this reduces retention time to 60 days. Note that Azure backup can only be used for servers running Windows Server 2008 R2 with SP1 or later and for Hyper\-V and SQL Server workloads.|Set from 1\-12 weeks|
|Synchronization frequency \- time<br /><br />How often incremental backups of the data sources run to synchronize the data replica on the DPM server with the protected resource|Set incremental backup from 15 minutes\-24 hours. 15 minutes is the default.|Not applicable.|
|Synchronization frequency – recovery point<br /><br />Express full backup runs just before each scheduled recovery point|Set express full backup to run before each scheduled recovery point|Not applicable.|
|Backup frequency|Not applicable|Set backup to run daily, weekly, or biweekly depending on the retention range.|
|Backup mode<br /><br />The type of backup to tape, and when it should run|Not applicable|Set full backup or full and incremental backup. Full and incremental is only available if you’ve set backup frequency to daily.<br /><br />Note that if you select incremental and full the actual retention range will be up to a week longer than the value you specify because of a dependency between full and incremental backups. Tapes with full backups will only be recycled after incremental backup tapes. For example with daily incremental and weekly full, the weekly full backup tape must wait forthe 6 daily incremental backup tapes to be recycled before the full backup tape is recycled|
|Data compression and encryption|Not applicable|You can encrypt data before it’s written to tape, and compress it on the tape|
|Recovery points—file data|Set days and times for creating recovery points. Backups for file data consist of synchronizations and recovery points only, and you can only recovery points can be recovered.|Set days and times for creating recovery points|
|Recovery points—application data|If the application supports incremental backup then recovery points will be created based on the setting you configured for the retention range \(for incremental backups\). If applications don’t support incremental backups each express full backup will create a recovery point for the application data.<br /><br />Express full backups synchronize by updating the data replica to apply block\-level changes to database files. These backups are only used applications that contain databases, such as Exchange, SQL and SharePoint. Synchronizations between express full backups replicate log files only. Both the express full and synchronization backups can be recovered. In contrast file data backups contain synchronizations and recovery points only, and only recovery points can be recovered.|If the application supports incremental backup then recovery points will be created based on the setting you configured for the retention range \(for incremental backups\). If applications don’t support incremental backups each express full backup will create a recovery point for the application data.|

### <a name="BKMK_Long"></a>Configure backups to long\-term storage

||Long\-term backup \(tape\)|
|-|------------------------------|
|Retention range<br /><br />How long data should be kept in short\-term storage|Set from 1\-99 years|
|Backup frequency|1\-99 years: Set daily, weekly, biweekly, monthly, quarterly, half\-yearly, yearly<br /><br />1\-\-\-11 months: Daily, weekly, biweekly, monthly<br /><br />1\-4 weeks: Daily, weekly|
|Backup mode<br /><br />The type of backup to tape, and when it should run|Set full backup or full and incremental backup. Full and incremental is only available if you’ve set backup frequency to daily.<br /><br />Note that if you select incremental and full the actual retention range will be up to a week longer than the value you specify because of a dependency between full and incremental backups. Tapes with full backups will only be recycled after incremental backup tapes. For example with daily incremental and weekly full, the weekly full backup tape must wait forthe 6 daily incremental backup tapes to be recycled before the full backup tape is recycled|
|Data compression and encryption|You can encrypt data before it’s written to tape, and compress it on the tape|
|Recovery points—file data|Set days and times for creating recovery points. Backups for file data consist of synchronizations and recovery points only, and you can only recovery points can be recovered.|
|Recovery points—application data|If the application supports incremental backup then recovery points will be created based on the setting you configured for the retention range \(for incremental backups\). If applications don’t support incremental backups each express full backup will create a recovery point for the application data.<br /><br />Express full backups are a type of synchronization that  a type of synchronization that updates the data replica to apply block\-level changes to database files. It’s only uses for applications that contain databases, such as Exchange, SQL and SharePoint. Then synchronizations between express full backups only replica log files.  Both the express full and synchronization backups are available for recovery.|

### <a name="BKMK_VM"></a>Configure backup windows for virtual machines
By default in DPM you schedule the start time for backup of a protection group but you don’t specify an end time. From DPM 201 R2 Update 3 onwards you can configure backup windows that specify when a backup job to short\-term disk storage should begin and end. This is currently only supported for virtual machines. Backup windows for other kinds of workloads in protection groups aren’t supported.

#### Create the backup window
Create the backup window with the following Windows PowerShell script

```
$pgName = $args[0]
$startTime = $args[1]
$duration = $args[2]
$pg = Get-ProtectionGroup -DPMServerName $env:computername | ?{$_.FriendlyName -like "*$pgName*"}
$mpg = Get-ModifiableProtectionGroup $pg

$sched = Get-DPMPolicySchedule -ProtectionGroup $mpg -ShortTerm | ? { $_.JobType -eq "FullReplicationForApplication" }
$sched

Set-DPMBackupWindow -ProtectionGroup $mpg -StartTime $startTime -DurationInHours $duration
Set-DPMPolicySchedule -ProtectionGroup $mpg -DaysOfWeek $sched.WeekDays -TimesOfDay $sched.TimesOfDay -Schedule $sched
Set-DPMConsistencyCheckWindow -ProtectionGroup $mpg -StartTime $startTime -DurationInHours $duration
Set-DPMProtectionJobStartTime -ProtectionGroup $mpg -JobType ConsistencyCheck -StartTime 02:00 -MaximumDurationInHours 3
set-dpmprotectiongroup $mpg

```

#### Retrieve backup window settings
Retrieve the backup window settings for a protection group with this Windows PowerShell script.

```
$pgName = $args[0]
Disconnect-DPMServer
Connect-DPMServer $env:computername
$pg = Get-ProtectionGroup | ?{$_.FriendlyName -like "*$pgName*"}
'Backup window'
Get-DPMBackupWindow $pg
'CC window'
Get-DPMConsistencyCheckWindow $pg

```

## <a name="BKMK_Demand"></a>Run on\-demand backups
In addition to schedule backups you can run an on\-demand backup of a data source in a protection group.

1.  In the protection group, right\-click the data source for which you want to run the backup.

    -   Select **Create recovery point – disk** if you want to run a backup to disk. You can select whether to run an express full backup or an incremental backup, if incremental is supported.

    -   Select **Create recovery point – tape** if you want to you run a backup to tape. You can select whether to synchronize first or not. For file data you can specify that you only want to synchronize without creating a recovery point.

    If you want to run an on\-demand backup for all data sources in a protection group, you can use the PowerShell script described in the DPM [blog](http://go.microsoft.com/fwlink/?LinkId=404312).

Note that if you want to run a single scheduled backup you need to create a new protection group to do it.

