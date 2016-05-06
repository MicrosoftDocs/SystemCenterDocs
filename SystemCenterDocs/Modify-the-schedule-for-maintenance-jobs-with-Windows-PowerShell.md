---
title: Modify the schedule for maintenance jobs with Windows PowerShell
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 272c923b-3ea3-401b-9a00-efa1a3b2e20f
---
# Modify the schedule for maintenance jobs with Windows PowerShell
You can set the schedules for maintenance jobs to be carried out on the DPM server only by using DPM Management Shell.

### To schedule a maintenance job

-   Use the following syntax to retrieve the current schedule for maintenance jobs to run on a DPM server:

    **Get\-MaintenanceJobStartTime \[\-DPMServerName\]** *<String>* **\[\-MaintenanceJob\]** *<HouseKeepingJobs>* **\[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to set the schedule for maintenance jobs to run on a DPM server:

    **Set\-MaintenanceJobStartTime \[\-DPMServerName\]** *<String>* **\[\-MaintenanceJob\]** *<HouseKeepingJobs>* **\[\[\-StartTime\]** *<DateTime>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to remove the schedule for maintenance jobs to run on a DPM server:

    **Set\-MaintenanceJobStartTime \[\-DPMServerName\]** *<String>* **\[\-MaintenanceJob\]** *<HouseKeepingJobs>* **\[\-Remove\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Set\-MaintenanceJobStartTime \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Set\-MaintenanceJobStartTime \-full**" in DPM Management Shell.

## See Also
[Modify the schedule for protection jobs with Windows PowerShell](../Topic/Modify-the-schedule-for-protection-jobs-with-Windows-PowerShell.md)
[Manage tapes](../Topic/Manage-tapes.md)

