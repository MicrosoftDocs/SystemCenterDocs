---
title: Modify the schedule for protection jobs with Windows PowerShell
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ef99b11-f540-41f9-9124-04163baaf76f
---
# Modify the schedule for protection jobs with Windows PowerShell
You can set the start time for protection jobs only by using DPM Management Shell. The protection jobs that you can reschedule are catalog pruning and detailed inventory.

### To schedule a protection job

1.  Use the following syntax to retrieve the current start time for a protection job:

    **Get\-ProtectionJobStartTime \[\-ProtectionGroup\]** *<ProtectionGroup>* **\[\-JobType\]** *<ProtectionJobType>* **\[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

2.  Use the following syntax to set the start time for a protection job:

    **Set\-ProtectionJobStartTime \[\-ProtectionGroup\]** *<ProtectionGroup>* **\[\-JobType\]** *<ProtectionJobType>* **\[\-StartTime\]** *<DateTime>* **\[\-MaximumDurationInHours\]** *<Int32>* **\[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

3.  Use the following syntax to remove the start time for a protection job:

    **Set\-ProtectionJobStartTime \[\-ProtectionGroup\]** *<ProtectionGroup>* **\[\-JobType\]** *<ProtectionJobType>* **\-Remove \[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Set\-ProtectionJobStartTime \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Set\-ProtectionJobStartTime \-full**" in DPM Management Shell.

## See Also
[Modify the schedule for maintenance jobs with Windows PowerShell](../Topic/Modify-the-schedule-for-maintenance-jobs-with-Windows-PowerShell.md)
[Understand data protection \[DPM2012\_Web\]](assetId:///ff928689-a0d9-4934-b791-d7fdeef931e6)

