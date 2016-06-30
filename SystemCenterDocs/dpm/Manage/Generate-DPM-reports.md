d|
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



