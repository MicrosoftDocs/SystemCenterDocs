---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Generate DPM reports
ms.technology:  data-protection-manager
ms.assetid:  f9a97135-1c5b-45a9-b307-bb957fde21d8
ms.author: markgal
---

# Generate DPM reports

>Applies To: System Center 2016 - Data Protection Manager

DPM uses SQL Server Reporting Services to create reports. In the **Reporting** task area you can generate and view reports, schedule automation report generation, managing settings, and subscribe to reports. Alternatively you can generate DPM reports from Operations Manager if you're using it to monitor DPM.

## DPM reports
DPM provides a number of different reports:

-   **Status report**: Provides the status of all recovery points for a specified time period. It lists recovery jobs, and shows the total number of successes and failures for recovery points and recovery point creation. You can use this report to track and verify recovery point metrics.

-   **Protection report**:  Provides commonly used metrics for backup success rolled up over long periods of time. Use this report to track how backups are doing and what's been backed up successfully.

-   **Recovery report**: Provides commonly used metrics for recovery success rolled up over long periods of time. Use this report  to track how recoveries are doing and how well you performed against your SLAs for RTOs.

-   **Disk utilization report**: Summarizes disk capacity, disk allocation, and disk usage in the DPM storage pool.
    Use this report to do the following:
    Identify trends in disk usage and make decisions about modifying space allocations.

-   **Tape management and tape utilization report**: Use the tape management report to track information about tape rotation and decommissioning, and to verify that the free media threshold hasn't been exceeded. Use the tape utilization report to track trending of resource (disk/tape) usage over time to assist capacity planning.

### Predefined SQL reports
DPM includes several SQL Server views to help you create custom reports. SQL views provide a simpler method that querying tables directly, by populating columns with data collected from multiple tables in the database. You don't need in-depth knowledge of the entire database or the relationship between tables and keys.

Note though that SQL views can degrade performance if used too frequently because the view runs each time it's queries. In addition the supported views might not include all the columns you need.

The following table summarizes the predefined SQL views.

|View|Field|Data type|Description|
|--------|---------|-------------|---------------|
|**Vw_DPM_Agents**<br /><br />Contains the list of computers on which a DPM protection agent from this DPM server is installed.|ServerName|String|The name of the computer|
|**Vw_DPM_Agents**|Version|String|DPM agent version on that computer|
|**Vw_DPM_Alerts**<br /><br />List of alerts from last 30 days|Severity|Integer<br /><br />0=Error<br /><br />1=Warning<br /><br />2=Information|Alert severity|
|**Vw_DPM_Alerts**|Resolution|Integer<br /><br />0 = Active<br /><br />1 = Recommended action in progress<br /><br />2 = Resolved|Alert state|
|**Vw_DPM_Alerts**|OccurredSince|Date and Time|First time alert was raised|
|**Vw_DPM_Alerts**|ResolvedTime|Date and Time|Time when alert was resolved|
|**Vw_DPM_Alerts**|Type|Integer|Alert type|
|**Vw_DPM_CurrentOnlineMedia**<br /><br />Tapes currently online in DPM owned libraries, as of the last inventory.|UserFriendlyName|String|Library name|
|**Vw_DPM_CurrentOnlineMedia**|ImportPoolMediaCount|Integer|Tapes imported to the DPM server|
|**Vw_DPM_CurrentOnlineMedia**|FreePoolMediaCount|Integer|Tapes marked as free or blank|
|**Vw_DPM_CurrentOnlineMedia**|AdminPoolMediaCount|Integer|Tapes with active data|
|**Vw_DPM_Disk_Usage_Replica**<br /><br />Disk usage statistics for replicas in the storage pool.|PhysicalPath|String|Protected data source name|
|**Vw_DPM_Disk_Usage_Replica**|ReplicaId|GUID|Unique identifier for replica|
|**Vw_DPM_Disk_Usage_Replica**|PGId|GUID|Unique identifier for protection group to which the data source belongs|
|**Vw_DPM_Disk_Usage_Replica**|ProductionServerName|String|Server on which data source is located|
|**Vw_DPM_Disk_Usage_Replica**|DiskAllocated|Big Integer|Total disk space allocated to data source|
|**Vw_DPM_Disk_Usage_Replica**|DiskUsed|Big Integer|Total disk space used by data source|
|**Vw_DPM_Disk_Usage_Replica**|FreeSpace|Big Integer|DiskAllocated - DiskUsed|
|**Vw_DPM_Disk_Usage_Replica**|ReplicaAllocated|Big Integer|Part of DiskAllocated reserved for replica of data source|
|**Vw_DPM_Disk_Usage_Replica**|ReplicaUsed|Big Integer|Part of ReplicaAllocated actually in use|
|**Vw_DPM_Disk_Usage_Replica**|ShadowCopyAllocated|Big Integer|Part of DiskAllocated reserved for recovery points of data source|
|**Vw_DPM_Disk_Usage_Replica**|ShadowCopyUsed|Big Integer|Part of ShadowCopyAllocated actually in use|
|**Vw_DPM_Disk_Usage_Replica**|StartDateTime|Date and time||
|**Vw_DPM_Disk_Usage_Replica**|EndDateTime|Date and time||
|**Vw_DPM_Disk_Usage_Replica**|ScheduleType|Integer<br /><br />0=weekly; 1=monthly; 2=quarterly; 3=yearly||
|**Vw_DPM_DiskRecoveryPoints**<br /><br />Counts for disk recovery points available for each data source.|DataSourceName|String|Protected data source name|
|**Vw_DPM_DiskRecoveryPoints**|PGId|GUID|Unique identifier for protection group to which data source belongs|
|**Vw_DPM_DiskRecoveryPoints**|ServerId|GUID|Unique identifier for server to which data source belongs|
|**Vw_DPM_DiskRecoveryPoints**|Frequency|Integer|Number of available recovery points|
|**Vw_DPM_LongRecoveries**<br /><br />Historical information about recoveries that took longer than 24 hours.|DataSourceName|String|The data source that was recovered|
|**Vw_DPM_LongRecoveries**|TargetServerName|String|The name of the server to which recovery was done|
|**Vw_DPM_LongRecoveries**|WriterId|GUID|Identifies the type of the data source that was recovered|
|**Vw_DPM_LongRecoveries**|StartTime|Date and time|The time at which the recovery was started|
|**Vw_DPM_LongRecoveries**|EndTime|Date and time|The time at which the recovery ended|
|**Vw_DPM_Media**<br /><br />Information about state of all tapes known to DPM.|MediaLabel|String|The label on the tape|
|**Vw_DPM_Media**|MediaBarcode|String|The barcode for the tape|
|**Vw_DPM_Media**|IsOnline|Integer|Whether the tape is online|
|**Vw_DPM_Media**|LibraryName|String|The name of the library in which the tape exists.<br /><br />NULL if tape is offline|
|**Vw_DPM_Media**|MediaSlotNumber|Integer|The slot number in which the tape exists.<br /><br />NULL if tape is offline<br /><br />If in a drive, this represents the home slot of the tape (to which the tape returns on a dismount).|
|**Vw_DPM_Media**|PGName|String|The name of the protection group in which the tape exists|
|**Vw_DPM_Media**|MediaExpiryDate|Date and time|The time when all data sets on this tape will expire.<br /><br />Can have the date in the past or NULL if the tape is free.|
|**Vw_DPM_MediaPool_Media**<br /><br />Tape counts for a given library.|LibraryName|String|The name of the library|
|**Vw_DPM_MediaPool_Media**|FreeMedia|Integer|Number of tapes that are free in this library|
|**Vw_DPM_MediaPool_Media**|FreeMediaThreshold|Integer|The threshold below which this library generates an alert|
|**Vw_DPM_ProtectedDataSource**<br /><br />Current disk space usage by various data sources.|ReplicaId|GUID|Identifier of the replica|
|**Vw_DPM_ProtectedDataSource**|PGId|GUID|Identifier of the protection group to which the replica belongs|
|**Vw_DPM_ProtectedDataSource**|AllocatedSize|Big integer|Disk space allocated to the data source|
|**Vw_DPM_ProtectedDataSource**|UsedSize|Big integer|Disk space currently used by the data source|
|**Vw_DPM_ProtectedDataSource**|ProductionServerName|String|The name of the computer on which the data source exists|
|**Vw_DPM_ProtectedDataSource**|StorageNode|String|Always set to the DPM server|
|**Vw_DPM_ProtectedGroup**<br /><br />Table with information about all protection groups.|PGId|GUID|Unique identifier for the protection group|
|**Vw_DPM_ProtectedGroup**|ProtectionGroupName|String|Protection group name|
|**Vw_DPM_ProtectedGroup**|CreationTime|Date and time|Time protection group was created|
|**Vw_DPM_RecoveryDuration**<br /><br />History of counts for recovery jobs in various time durations.|StartDateTime|Date and time|The time at which the statistic was collected|
|**Vw_DPM_RecoveryDuration**|EndDateTime|Date and time|Internal|
|**Vw_DPM_RecoveryDuration**|ScheduleType|Integer|The frequency for which this particular statistic was collected|
|**Vw_DPM_RecoveryDuration**|RecoveryDuration|Integer|Indicates if the recovery was less than 6 hours, between 6-24 hours, or greater than 24 hours|
|**Vw_DPM_RecoveryDuration**|RecoveryCount|Integer|Number of recoveries|
|**Vw_DPM_RecoveryJob**<br /><br />Detailed information about recent recovery jobs.|DataSourceName|String|The data source for which recovery was run|
|**Vw_DPM_RecoveryJob**|ServerName|String|The server to which recovery was performed|
|**Vw_DPM_RecoveryJob**|CreationTime|Date and time|Time at which the recovery job was run|
|**Vw_DPM_RecoveryJob**|FailureCode|Integer|Error code in case of failure of the recovery job|
|**Vw_DPM_RecoveryJob**|Status|Integer<br /><br />0/1=Progress<br /><br />2=Succeeded<br /><br />3=Failure|Status of the recovery job|
|**Vw_DPM_RecoveryPointDisk**<br /><br />Status of recent recovery point creation jobs on disk.|String|The data source for which the backup was created|String|
|**Vw_DPM_RecoveryPointDisk**|String|The server on which the data source exists|String|
|**Vw_DPM_RecoveryPointDisk**|Date and time|The time at which the recovery point creation job was run|Date and time|
|**Vw_DPM_RecoveryPointDisk**|Integer<br /><br />0/1=Progress<br /><br />2=Succeeded<br /><br />3=Failure|Status of the recovery point creation job|Integer<br /><br />0/1=Progress<br /><br />2=Succeeded<br /><br />3=Failure|
|**Vw_DPM_RecoveryPointDisk**|Integer|Zero if succeeded.<br /><br />Else, set to a DPM error code.|Integer|
|**Vw_DPM_RecoveryPointTape**<br /><br />Status of recent recovery point creation jobs on tape.||||
|**Vw_DPM_RecoveryPointTape**|String|The data source for which the backup was created|String|
|**Vw_DPM_RecoveryPointTape**|String|The server on which the data source exists|String|
|**Vw_DPM_RecoveryPointTape**|Date and time|The time at which the recovery point creation job was run|Date and time|
|**Vw_DPM_RecoveryPointTape**|Integer<br /><br />0/1=Progress<br /><br />2=Succeeded<br /><br />3=Failure|Status of the recovery point creation job|Integer<br /><br />0/1=Progress<br /><br />2=Succeeded<br /><br />3=Failure|
|**Vw_DPM_Replica**<br /><br />Listing of all replicas managed by DPM|ReplicaId|GUID|Unique identifier generated by DPM for the replica volume|
|**Vw_DPM_Replica**|PhysicalPath|String|The name of the data source on the replica|
|**Vw_DPM_Replica**|ServerName|String|Name of the server to which the data source belongs|
|**Vw_DPM_Replica**|ValidFrom|Date and time|When the replica was created|
|**Vw_DPM_Replica**|ValidTo|Date and time|The date on which the replica was made inactive|
|**Vw_DPM_Replica**|PGId|GUID|Unique identifier generated by DPM for the protection group to which the data source belongs|
|**Vw_DPM_Replica**|StorageNode|String|Always set to the DPM server|
|**Vw_DPM_Server**<br /><br />List of all protected computers.|ServerId|GUID|Unique identifier generated by DPM for the protected computer|
|**Vw_DPM_Server**|ServerName|String|Fully qualified domain name for the computer|
|**Vw_DPM_Server**|NetBiosName|String|Name|
|**Vw_DPM_Server**|DomainName|String|Domain in which the computer belongs|
|**Vw_DPM_Server**|IsRG|Integer|If this computer represents a Resource Group|
|**Vw_DPM_TapeRecoveryPoints**<br /><br />Counts for tape recovery points available for each data source.|DataSourceName|String|The name of the protected data source|
|**Vw_DPM_TapeRecoveryPoints**|PGId|GUID|The unique identifierentifier for the protection group to which this data source belongs|
|**Vw_DPM_TapeRecoveryPoints**|ServerId|GUID|The unique identifierentifier for the server to which this data source belongs|
|**Vw_DPM_TapeRecoveryPoints**|Frequency|Integer|The number of available recovery points|
|**Vw_DPM_TapeRecoveryPoints**|Term|Integer<br /><br />0=ShortTerm; 1=LongTerm|The schedule to which the recovery point corresponds|
|**Vw_DPM_TapeStat**<br /><br />Historical information on tape usage counts.|StartDateTime|Date and time||
|**Vw_DPM_TapeStat**|EndDateTime|Date and time||
|**Vw_DPM_TapeStat**|ScheduleType|Integer|Integer<br /><br />0=Weekly<br /><br />1=Monthly<br /><br />2=Quarterly<br /><br />3=Yearly|
|**Vw_DPM_TapeStat**|Free|Integer|Number of free tapes at end-time|
|**Vw_DPM_TapeStat**|Online|Integer|Number of online tapes at end time|
|**Vw_DPM_TapeUsagePerPG**<br /><br />Historical tape usage data per protection group.|StartDateTime|Date and time|Start time|
|**Vw_DPM_TapeUsagePerPG**|EndDateTime|Date and time|End time|
|**Vw_DPM_TapeUsagePerPG**|PGName|String|Name of the protection group|
|**Vw_DPM_TapeUsagePerPG**|ScheduleType|Integer|Integer<br /><br />0=Weekly<br /><br />1=Monthly<br /><br />2=Quarterly<br /><br />3=Yearly|
|**Vw_DPM_TapeUsagePerPG**|Online|Integer|Number of online tapes at end time|
|**Vw_DPM_TapeUsagePerPG**|Offline|Integer|Number of offline tapes at end time|
|**Vw_DPM_Total_Disk_Trend**<br /><br />Total disk space usage historical trend.|StartDateTime|Date and time||
|**Vw_DPM_Total_Disk_Trend**|EndDateTime|Date and time||
|**Vw_DPM_Total_Disk_Trend**|ScheduleType|Integer|Integer<br /><br />0=Weekly<br /><br />1=Monthly<br /><br />2=Quarterly<br /><br />3=Yearly|
|**Vw_DPM_Total_Disk_Trend**|DiskSpaceCapacity|Big integer|The total storage in storage pool at end-time|
|**Vw_DPM_Total_Disk_Trend**|PreviousDiskSpaceCapacity|Big integer|Total storage in storage pool in previous corresponding period|
|**Vw_DPM_Total_Disk_Trend**|DiskSpaceAllocated|Big integer|The disk space from storage pool that has been allocated|
|**Vw_DPM_Total_Disk_Trend**|PreviousDiskSpaceAllocated|Big integer|The disk space from storage pool that was allocated in the previous corresponding period|
|**Vw_DPM_Total_Disk_Trend**|DiskSpaceUsed|Big integer|The actual disk space usage|
|**Vw_DPM_Total_Disk_Trend**|PreviousDiskSpaceUsed|Big integer|The used disk space in the previous corresponding period|
|**Vw_DPM_Total_RecoveryPoint**<br /><br />Information about all recent recovery point jobs.|DataSourceName|String|The name of the protected data source|
|**Vw_DPM_Total_RecoveryPoint**|ServerName|String|The server to which the data source belongs|
|**Vw_DPM_Total_RecoveryPoint**|CreationTime|Date and time|The time at which the recovery point creation job was run|
|**Vw_DPM_Total_RecoveryPoint**|Status|Integer<br /><br />0/1=Progress<br /><br />2=Succeeded<br /><br />3=Failure|Status of the recovery point creation job|
|**Vw_DPM_Total_RecoveryPoint**|ErrorCode|Integer|Error code in recovery point creation|

### Set up reports

#### Schedule reports
Reports aren't scheduled by default in DPM. To start creating and saving historical reports you create a report schedule. Each report type has an independent schedule A report only has a single schedule. Schedule a report as follows:

1.  In DPM Administrator Console, go to the **Reporting** view. On the display pane, select the report and click **Schedule**.

2.  Select **Run the <name of report> according to the schedule options**.

3.  On the **Schedule** tab, select schedule options, including frequency, how to group, the time of the day to generate, and the granularity. Granularity is limited by frequency. So, if the frequency is weekly, then so is the granularity, the time period to be included in the report data, and the number of copies to retain in history.

### View reports
In the DPM Administrator Console you can display both new and historical reports in Internet Explorer. You can use the Reporting Services Web toolbar at the top of report to customize, export or print it.

1.  You can request a new report with the following settings:

    -   Display - You can view a report groups by protected computer or protection group.

    -   You can specify or exclude a specific time period. You can set report granularity as follows:

        -   Week - Seven days - from Sunday through Saturday

        -   Month - A full month from the first to the last day of the month

        -   Quarterly - For three months starting from January (e.g January through March.

        -   Annual - January 1 to December 31 of a particular year.

2.  You can view an available report from the **Available reports** list. When the number of historical reports saved equals the maximum number specified in the report schedule, the next report that is saved will replace the oldest copy of the report, so you can retain the maximum number of copies at all times.

### Print reports
Reports in DPM have been designed to print on A4 paper without horizontally splitting the information across pages. The MHTML and PDF formats are not editable, so you can't modify the report to fit other paper sizes.

Note that if you experience any issues with reports on fitting on A4 paper try changing the dimensions of the report page width 8.27in and the height to 11.69in. There are details of how to do that on Bob Cornelissen's [BICTT blog](http://www.bictt.com/blogs/bictt.php/2009/03/17/sql-reporting-services-render-pdf-in-a4-1).

##### Print MHTML reports

1.  On the Internet Explorer **File** menu, click **Page Setup**.

2.  Set paper size to A4 and select **Orientation** > **Portrait**.

3.  Set **Margins** to values no greater than the following (in inches): **Left:** 0.11, **Right:** 0.11, **Top:** 0.11, **Bottom:** 0.11. Then print the report.

##### Print a PDF report

1.  In Adobe Acrobat, open the **Print** dialog box.

2.  Set **Page Scaling** to **Shrink large pages** (the default setting). Select **Auto-Rotate and Center**.

3.  On the **Advanced** tab, set the orientation to **Portrait** and print the report.

##### Print a report using Microsoft Excel

1.  Open the file in Excel.

2.  Click **Page Layout** > **Orientation** > **Portrait**.

3.  Click **Size** > **A4** .

4.  Click **Margins** > **Custom Margins**. Set the **Top**, **Left**, **Bottom**, and **Footer** margins to 0.

5.  In **Scale to Fit** set  **Scale** to 80%.

6.  In **Sheet Options** clear **Print** if it's selected. Then print the report.

### Send reports
You can send reports to subscribers via email. Reports are sent as file attachments. To subscribe to reports do the following:

1.  Specify the SMTP server that DPM will use to send reports.

2.  In the Reporting view, on the display pane right-click the report to which you want to subscribe and click **Schedule**.

3.  On the **E-mail** tab, in **Recipients** type the e-mail addresses of all the subscribers. Only add email addresses that are relevant on the designed server, and separate addresses with a comma. Then select the format.

## Generate DPM reports in Operations Manager
Operations Manager provides an Operations console and a web console that you can use to view and work with the monitoring data for your environment. To retrieve information you can use predefined views, or search for data and objects using searching and filtering. For more information, see [Getting Information from Operations Manager](https://technet.microsoft.com/en-us/library/hh212876.aspx).
DPM provides a number of predefined views that you can use to search more simply than defining your own query or filter.

DPM provides a number of predefined views that you can use to search more simply than defining your own query or filter.

**View Name:**  vDPMBackupJob (Shows backup job details):

|Field|Data type|Description|
|---------|-------------|---------------|
|BackupJobRowId|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|TaskID|uniqueidentifier|Task identifier to uniquely identify job|
|VerbID|uniqueidentifier|Identifies the job type|
|ProtectionServer|varchar(max)|The protection server or cluster against which the job ran|
|ProtectionGroupID|uniqueidentifier|The protection group ID for which the job ran|
|ProtectionGroup|varchar(max)|Name of protection group|
|DataSourceID|uniqueidentifie|Date source ID for which the job ran|
|DataSourceName|varchar(max)|Data source name|
|StartedDateTime|datetime|Time job startedd|
|StoppedDateTime|datetime|Time job stopped|
|ExecutionState|int|2 = Succeeded; 3 = Failed|
|ErrorCode|int|Error code for job failure. Error code can be ignored if job succeeded|
|ErrorString|varchar(max)|Corresponding localized error string|
|TransferredBytes|int|Number of bytes transferred by the job|
|BackupType|varchar(max)|DiskBackup; TapeBackup; CloudBackUp|
|IsDPM|bit|Whether job ran again a DPM server (indicating it ran on secondary DPM server)|
|IsAdHoc|bit|Whether job is ad hoc or scheduled|

**View Name:** vDPMRecoveryJob (Recovery job details):

|Field|Data type|Description|
|---------|-------------|---------------|
|RecoveryJobRowID|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|TaskID|uniqueidentifier|Task identifier to uniquely identify job|
|DatasourceID|uniqueidentifier|Data source ID for which the recovery job ran|
|DataSourceName|varchar(max)|Data source for which the recovery job ran|
|StartedDateTime|datetime|Job start time|
|StoppedDateTime|datetime|Job end time|
|ExecutionState|Int|2=succeeded; 3=failed|
|ErorCode|int|Error code. If job succeeded ignore the error.|
|ErrorString|varchar(max)|Corresponding localized error string|
|TransferredBytes|int|Number of bytes transferred by the job|
|RecoverySource|int|0 = disk; 1 = Tape; 2 = Cloud|
|RecoveryType|int|Indicates recovery type|
|TargetServerName|varchar(max)|Target server on which the recovery was performed|
|TargetLocation|varchar(max)|Folder path to which recovery was performed|
|IsExternalSource|int|Indicates whether the data source is external (for example from a tape imported from another DPM server)|

**View Name:**  vDPMDiskManagement (Shows disk management information):

|Field|Data type|Description|
|---------|-------------|---------------|
|DiskManagementRowID|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|DiskID|uniqueidentifier|Unique ID to identify disk|
|DiskName|varchar(max)|Name of disk returned by VDS APIs (for example "Microsoft Virtual Disk"|
|TotalSize|bigint|Total size of disk|
|FreeSize|bigint|Free size on disk|
|IsInStoragePool|bit|Indicates whether the disk belongs to the DPM storage pool|
|DiskType|smallint|0 = basic, 1 = dynamic; 2 = uninitialized|
|HealthStatus|smallint|0 = healthy; 1 = failed|
|IsMissing|bit|Indicates whether the disk is missing|
|IsForeign|bit|Indicates whether the disk is foreign|
|CanAddToStoragePool|bit|Indicates whether the disk can be added to the DPM storage pool|
|CreatedDateTime|datatime|Created time|

**View Name:** vDPMDiskUtlization (Shows disk statistics):

|Field|Data type|Description|
|---------|-------------|---------------|
|DiskUtilizationRowID|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|SMStatsID|uniqueidentifier|Statistics identifier used inside DPM|
|DataSourceID|uniqueidentifier|Data source ID for which the job ran|
|DataSourceName|varchar(max)|Data source for which the job ran|
|ProductionServer|varchar(max)|Server or cluster to which the data source belongs|
|ProtectionGroupID|uniqueidentifier|ID of protection group to which the data source belongs|
|ProtectionGroup|varchar(max)|Name of protection group to which the data source belongs|
|ReplicaSpaceAllocated|bigint|Total size of replica volume|
|ShadwoCopyAllocatedSize|bigint|Shadow copy volume size|
|ShadowCopyUsedSize|bigint|Used size of shadow copy volume|
|ReplicaUsedSize|bigint|Used size of the replica volume|
|FreeSpaceAvailable|bigint|Total free space on replica and shadow copy volumes|
|IsCollocated|int|Indicates whether the volume is used for a collocated protection group that might have multiple data sources|

**View Name:** vDPMSLATrend (Useful to show the percentage of instances where SLA was or wasn't met):

|Field|Data type|Description|
|---------|-------------|---------------|
|SLATrendRowId|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|SMStatsID|uniqueidentifier|Statistic identifier used in DPM|
|StartTime|datetime|Start time of specific SLA period|
|EndTime|datetime|End time of specific SLA period|
|DatasourceID|uniqueidentifier|ID of the data source for which the job ran|
|DatasourceName|varchar(max)|Name of the data source for which the job ran|
|ProtectionServer|varchar(max)|The server or cluster to which the data source belongs|
|ProtectionGroupID|uniqueidentifier|The ID of the protection group to which the data source belongs|
|ProtectionGroupName|varchar(max)|The protection group to which the data source belongs|
|CreationTime|datetime|Time that the statistic was created|
|DiskRecoveryPointAvailable|bit|Indicates whether there's a disk recovery point available in the SLA period|
|TapeRecoveryPointAvailable|bit|Indicates whether there's a tape recovery point available in the SLA period|
|CloudRecoveryPointAvailable|bit|Indicates whether there's a cloud recovery point available in the SLA period|
|SLA|int|Indicates the SLA for the protection group during this SLA period|

**View Name:** vDPMTapeUtilization (Shows DPM Tape Utilization):

|Field|Data type|Description|
|---------|-------------|---------------|
|TapeUtilizationRowId|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|SMStatsID|uniqueidentifier|Unique statistics identifier in DPM|
|StartTime|datetime|Start time of statistics period|
|EndTime|datetime|End time of statistics period|
|FreeTapeCount|int|Number of free tapes attached to the DPM server|
|OnlineTapeCount|int|Number of online tapes attached to the DPM server|
|OfflineTapeCount|int|Number of offline tapes attached to the DPM server|

**View Name:** vDPMTapeManagement (Shows DPM information for tape libraries and tape identification):

|Field|Data type|Description|
|---------|-------------|---------------|
|TapeManagementRowID|uniqueidentifier|Index key|
|DPMServerName|varchar(max)|DPM server|
|MediaSlotNumber|int)|Slot number of the library on which the media is present|
|MediaBarcode|varchar(max)|Barcode of the tape|
|MediaLabel|varchar(max)|Label of the tape|
|IsOnline|bit|Indicates whether the tape is online|
|LibraryName|varchar(max)|Name of the library|
|ProtectedGroupName|varchar(max)|Name of the protection group that owns the tape|
|MediaExpiryDate|datetime|Expiry date of the tape|
