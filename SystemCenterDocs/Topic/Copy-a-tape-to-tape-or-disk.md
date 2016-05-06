---
title: Copy a tape to tape or disk
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49da65a3-abed-4f79-8c51-db8c3d5bd4c6
---
# Copy a tape to tape or disk
Use the following procedures in DPM to copy a tape. When you configure a protection group to use tape\-based protection, you can specify how many copies of each tape that DPM should create. However, you can also copy the tapes manually.

### Copy a tape to disk

1.  In DPM Administrator Console, go to the **Management** view, and then open the **Libraries** workspace.

2.  In the display pane, expand the tape library or stand\-alone tape drive, select the tape that you want to copy, and then click **View tape contents**.

3.  In the tape contents dialog box, select the data to be copied, and then click **Copy**.

4.  In the **Specify Alternate Recovery Destination** dialog box, specify a destination on a computer that has the protection agent installed, and then click **OK**.

5.  Click **Yes** to proceed with the copy operation.

6.  Click **OK** to close the message.

7.  You can view the progress of the copy job in the **Monitoring** task area on the **Jobs** tab.

### Copy a tape to another tape

1.  In DPM Administrator Console, go to the **Recovery** view.

2.  Select the data that you want to copy to tape, and then click **Recover**. The Recovery Wizard opens.

3.  On the **Review Recovery Selection** page, you can confirm which tape or tapes the data is on. Click **Next** to continue.

4.  On the **Specify Recovery Type** page, select the copy to tape option, and then click **Next**.

5.  On the **Specify Library** page, in **Primary library**, select a library to use for recovery.

    1.  When the data is being copied from tape and the tape library has multiple tape drives, the library you select in **Primary library** reads from the source tape and copies the data to another tape.

    2.  When the data is being copied from tape and the tape library has only a single tape drive, the library you select in **Primary library** reads from the source tape and the library you select in **Copy library** copies the data to tape.

6.  On the **Specify Recovery Options** page, you can specify e\-mail addresses to receive notification upon completion of the recovery. Click **Next** to continue.

7.  On the **Summary** page, review the settings and then click **Recover**.

### To copy a tape using DPM Management Shell

-   Use the following syntax to copy a tape:

    **Copy\-DPMTapeData \[\-RecoveryPoint\]** *<RecoverySource>* **\-SourceLibrary** *<Library>* **\-TargetLibrary** *<Library>* **\-TapeLabel** *<String>* **\-TapeOption** *<TapeOptions>* **\[\-RecoveryPointLocation** *<RecoverySourceLocation>***\] \[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to copy the recovery points from a tape:

    **Copy\-DPMTapeData \[\-RecoveryPoint\]** *<RecoverySource>* **\[\-RecoveryPointLocation** *<RecoverySourceLocation>***\] \-Tape** *<Media>* **\[\-Restore\] \-OverwriteType** *<OverwriteType>* **\[\-RecreateReparsePoint\] \[\-RestoreSecurity\] \-TargetServer** *<String>* **\-TargetPath** *<String>* **\[\-RecoveryNotification** *<NotificationObject>***\] \[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable***<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to copy headless data from a tape:

    **Copy\-DPMTapeData \-IncompleteDataset** *<HeadlessDataset>* **\-Tape***<Media>* **\[\-Restore\] \-OverwriteType** *<OverwriteType>* **\[\-RecreateReparsePoint\] \[\-RestoreSecurity\] \-TargetServer** *<String>* **\-TargetPath** *<String>* **\[\-RecoveryNotification** *<NotificationObject>***\] \-DPMServerName** *<String>* **\[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Copy\-DPMTapeData \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Copy\-DPMTapeData \-full**" in DPM Management Shell.

