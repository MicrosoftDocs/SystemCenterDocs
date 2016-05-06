---
title: Recover system state or BMR
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b81e94-584b-40a4-b14c-262ebc8e98a8
---
# Recover system state or BMR
If you’ve backed up system state or bare metal recovery \(BMR\) of servers with DPM, if the server stops working you can restore BMR or system state, as follows:

1.  Recover the BMR or system state backup to a network location.

2.  If you’ve backed up BMR use the Windows Recovery Environment \(WinRE\) to start up your system and connect it to the network. Then use Windows Server Backup \(WSB\) to recover your system information from the network location.

3.  If you’ve backed up system state use Windows Server Backup \(WSB\) to recover your system information from the network location.

## Restore BMR
You’ll need to:

-   Run recovery on the DPM server

-   Set up the share—We’re recovering to a network share \(folder on the protected computer\) so you’ll need to create a folder.  Before you start remember that you’ll need access to the share location from the WinRE environment. WinRE will need network address \(IP address\) and will need to specify valid credentials for share access. Note that WinRE can’t connect to network shares that have IPsec enabled. The computer should be an IPsec boundary computer so that a computer that isn’t joined to a domain can access the network share using a user name and password.

-   Restore the system— After you’ve recovered to a network location you’ll restore the system from the protected server using WinRE.

#### Run recovery on the DPM server

1.  In DPM Administrator Console > **Recovery** find the server you want to restore and find the **Bare Metal Recovery** option.

2.  Available recovery points are indicated in bold on the calendar in the recovery points section. Select the data and time for the recovery point you want to recover.

3.  In the **Select Recovery Type** page of the Recovery Wizard, click select **Copy to a network folder**.

4.  On the **Specify Destination** page, select where you want to copy the data to.

    We recommend that you use a new folder to recover the system information. This will make it easier for you to point WSB to the right folder for recovery. Remember that the destination must have enough room.

5.  On the Specify Recovery Options page select to apply the security settings of the destination computer, and select **Enable SAN based recovery using hardware snapshots** if you want to use SAN\-based hardware snapshots for quicker recovery.

    This option is valid only if you have a SAN with hardware snapshot functionality enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the DPM server are connected to the same SAN.

    In **Notification** you can specify to **Send an e\-mail when the recovery completes**, and the email recipients. Separate the addresses with commas.

6.  On the **Summary** page review the settings and click **Recover**.

    You can follow the recovery process on the **Monitoring** tab. Any synchronization jobs for the selected recovery item is canceled while the recovery is in progress.

#### Set up the share

1.  Navigate to the restore location and find the folder in whih the backup is stored.  Share the folder above WindowsImageBackup so that at the root of the shared folder is the WindowsImageBackup folder. If it isn’t at the root the restore won’t find the backup.

    To connect using WinRE it’s essential to create the share that you can access in WinRE with correct IP address connectivity and credentials\), and that the  WindowsImageBackup folder is on the root of the share.

#### Restore the system

1.  Start the computer for which you want to restore the image to using the Windows DVD to match the system you are restoring.

2.  On the first screen verify language\/locale settings and click **Next**.

3.  On the **Install** screen comes up, select **Repair your computer**.

4.  On the **System Recovery Options** page select **Restore your computer using a system image that you created earlier** > **Next**.

5.  On the **Select a system image backup** screen select **Select a system image** > **Advanced** > **Search for a system image on the network**.  Select **Yes** if a warning appears. Navigate to the share path, input the credentials, and select the recovery point.

6.  This scans for specific backups available in that recovery point. Select the recovery point and click **Next**.

7.  In **Choose how to restore the backup** select **Format and repartition disks**. In the next screen verify settings and click **Finish** to begin the restore. Restart as required.

## Restore system state

#### Run recovery on the DPM server

1.  In DPM Administrator Console > **Recovery** find the server you want to restore and find the **Bare Metal Recovery** option.

2.  Available recovery points are indicated in bold on the calendar in the recovery points section. Select the data and time for the recovery point you want to recover.

3.  In the **Select Recovery Type** page of the Recovery Wizard, click select **Copy to a network folder**.

4.  On the **Specify Destination** page, select where you want to copy the data to.

    We recommend that you use a new folder to recover the system information. This will make it easier for you to point WSB to the right folder for recovery. Remember that the destination must have enough room.

5.  On the Specify Recovery Options page select to apply the security settings of the destination computer, and select **Enable SAN based recovery using hardware snapshots** if you want to use SAN\-based hardware snapshots for quicker recovery.

    This option is valid only if you have a SAN with hardware snapshot functionality enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the DPM server are connected to the same SAN.

    In **Notification** you can specify to **Send an e\-mail when the recovery completes**, and the email recipients. Separate the addresses with commas.

6.  On the **Summary** page review the settings and click **Recover**.

    You can follow the recovery process on the **Monitoring** tab. Any synchronization jobs for the selected recovery item is canceled while the recovery is in progress.

#### Share out the folder

1.  Set share permissions on the folder so that WSB can access it.

#### Run WSB on the protected server

1.  Click **Actions** > **Recover** > **This Server** > **Next**.

2.  Click **Another Server** > **Specify Location Type**page > **Remote shared folder**. Provide the path to the folder that contains the recovery point and click **Next**.

3.  On the **Select Recovery Type**page, click **System state** > **Next.**

4.  On the **Select Location for System State Recovery**page, click **Original Location** > **Next**.

5.  On the **Confirmation**page, click **Recover**.You’ll need to restart the server after the restore.

6.  You can also run a system state restore from the command line:

7.  1.  Start the server you want to recover and start WSB.

    2.  Open a command prompt and get the version identifier: **wbadmin get versions –backuptarget <servername\\sharename>**

    3.  Use the version identifier to start system state restore. At the command line type: **wbadmin start systemstaterecovery –version:<versionidentified> –backuptarget:<servername\\sharename>**

        Confirm that you want to start the recovery. You can see the process in the command window. A restore log is created. You’ll need restart the server after the restore.

