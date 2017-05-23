---
ms.assetid:
title: Release Notes for System Center DPM 2016
description: The system requirements article provides general performance and scalability guidance for consideration as part of your design planning of.
author: markgalioto
ms.author: markgal
manager: carmonm
ms.date: 05/23/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: data-protection-manager
ms.topic: article
---

# Release Notes for System Center Data Protection Manager (DPM) 2016

>Applies To: System Center 2016 - DPM

The following set of notes lists known issues and steps to mitigate the issue. These notes only apply to System Center DPM 2016.  

## Backups for Windows 10 Anniversary Update clients

**Description**: Some backup jobs for DPM-protected Windows 10 clients may not start after updating the client with the Anniversary update.

**Workaround**: On the client computer:

1. Open the Task Scheduler app.

2. In the Task Scheduler library, find and select the scheduled job, **ScheduledDPMClientBackup**.

3. In the **Actions** pane, click **Export** and save the xml output as a backup copy.

4. In the **Actions** pane, click **Properties**.

  The properties dialog box for ScheduledDPMClientBackup opens.

5. In the **Properties** dialog, select the **Triggers** tab, and click **Edit**.

6. In the **Edit Trigger** dialog, from the **Begin the task** drop-down menu, select **At log on**.

7. In **Advanced settings**, check **Repeat task every** and select **15 minutes**. From the **for a duration of** menu, select **Indefinitely**, and then click **OK**.

8. You must reboot the computer for these changes to take effect.



## Silent Installation of System Center DPM with SQL Server 2008

**Description**: You cannot silently install DPM 2016 RTM on SQL Server 2008.

**Workaround**: Deploy DPM 2016 RTM on a version of SQL Server higher than 2008, or use the DPM 2016 Setup UI


## Hyper-V VMs are protected twice on VM upgrade

**Description**: If you upgrade your Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016 to enable Resilient Change Tracking (RCT), a new VM representing the upgraded VM may appear in the Create Protection Group Wizard. The 2016 version of the VM may appear in addition to the 2012 R2 version of the VM.

**Workaround**: For the VMs that have not been upgraded, stop protection with Retain Data. After upgrading the VM, create a new protection group. Then, refresh the data sources and protect the VMs. This protects the VMs using Resilient Change Tracking (RCT).

## Agent installation fails on Windows Server 2008, Windows Server 2008 R2

**Description**: If you are trying to protect Windows Server 2008, or Windows Server 2008 R2, agent installation may fail.

**Workaround**: Upgrade the Windows Management Framework (WMF) on the production server to 4.0. Download the WMF from [https://www.microsoft.com/download/details.aspx?id=40855](https://www.microsoft.com/download/details.aspx?id=40855). Install WMF and then install the agent.


## Restoring a previous version of an upgraded Hyper-V VM causes future recovery points to fail.

**Description**: If you upgrade a protected 2012 R2 Hyper-V VM to the 2016 version, then stop protecting the VM (but retain data), and then re-enable protection, if you then recover a 2012 R2 copy at the original location, further backups may fail.

**Workaround**: After recovery change the VM Version to 2016 followed by a Consistency Check.


## Bare Metal Recovery protection failures

**Description**: If you configure Bare Metal Recovery (BMR) protection, the BMR protection job may fail with the message that the replica size is not sufficiently large.

**Workaround**: Use the following registry path to change the default replica size for BMR data sources. Open the registry editor and increase the replica size for the the following key: 
```
HKLM\Software\Microsoft\Microsoft Data Protection Manager\Configuration ReplicaSizeInGBForSystemProtectionWithBMR (DWORD)
```

## Re-protecting the DPM database after upgrading to DPM 2016

**Description**: When you upgrade from System Center DPM 2012 R2 to System Center Data Protection Manager 2016, the DPM database name can change in some scenarios.

**Workaround**: If you are protecting DPM DB, please ensure that you enable protection for new DPM DB. Protection for the old DPM DB can be removed once DPM upgrade is validated.


## Hyper-V RCT - recover as files for D-T backup fails

**Description**: Recovery of Hyper-V RCT VMs as files created directly on tape (D-T) fails. D-D-T backups will not exhibit this issue.

**Workaround**: Do Alternate Location Recovery as a VM, and then transfer those files to the desired location.



## Next steps
To install DPM, see the article, [Install DPM](install-dpm.md).

If you would like to consult planning information for your environment, see [Preparing your environment for System Center 2016 Data Protection Manager](prepare-environment-for-dpm.md).
