---
title: Recover data from tapes
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81726a92-5836-4825-b3ae-1f5d90b7145f
---
# Recover data from tapes
To recover data from tapes, first verify that data is recoverable, and then recover it.

## Verify data is recoverable
The **Verify tape** action verifies whether the selected recovery point on tape is recoverable. During verification, DPM mounts and reads the tape on which the data exists. You can monitor the progress of verification in the **Monitoring** task area on the **Jobs** tab. If the selected recovery point is stored on tape that is not in the tape library, DPM will queue the job for one hour. You must add the tape that contains the selected recovery point to the library within the one hour timeframe or the job will expire.

Verify as follows:

1.  In DPM Administrator Console, go to the **Recovery** view.

2.  Select a recovery point that is on tape.

3.  Click **Verify tape** from the tool ribbon.

#### Verify data with Windows PowerShell

-   Use the following syntax to verify the data on a tape:

    **Test\-DPMTapeData \[\-RecoveryPoint\]** *<RecoverySource>* **\[\-RecoveryPointLocation** *<RecoverySourceLocation>***\] \[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Test\-DPMTapeData \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Test\-DPMTapeData \-full**" in DPM Management Shell.

## Recover data from expired tapes
DPM doesn’t allow you to recatalog a tape that has expired but you can recover data from such a tape as follows:

1.  On the Administrator Console, right\-click the expired tape, and then click **Mark tape as free**. This changes the status of the tape to **Free \(contains data\)**.

    Right\-click the tape again and then click **Unmark tape as free**. This changes the status of the tape to **Imported <original tape label>**.

2.  Right\-click the tape again and then click **Recatalog imported tape**. After you recatalog the contents of an expired tape, the recovery points from this tape will appear as **External DPM Tapes** on the **Recovery** tab.

## Recover data from tapes created by another DPM server
To recover data from tapes created by another DPM server you’ll need to physically add the tape to a DPM server and then use the **Recatalog imported tape** action.

During the recatalog operation, DPM reads from the tape and adds information about the data it contains to the database. After recatalog completes, you can recover data from the tape by selecting a recovery point from the data on the tape.

## Recover data when a tape set is missing a tape
When protected data, such as a volume or a SQL Server database, spans multiple tapes, all tapes from the tape set must be available for DPM to recover the data. Recover data as follows:

1.  Add the tape to the tape set. You might need to recatalog the tape.

2.  View the contents of the tape.

3.  Copy the contents of the tape to the desired location.

After you copy the contents of the remaining tapes, you can use the copied data as you like.


