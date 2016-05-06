---
title: Manage tape libraries
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7f1b054-1c64-4a32-a418-014cf0088f60
---
# Manage tape libraries
Use the following procedures to manage tapes in the DPM library:

-   [Enable or disable a library](#BKMK_Enable)

-   [Detect tape drives](#BKMK_Detect)

-   [Rename a tape library](#BKMK_Rename)

-   [Lock or unlock a library door](#BKMK_Lock)

-   [Clean a tape drive](#BKMK_Clean)

## <a name="BKMK_Enable"></a>Enable or disable a library or drive
You can temporarily disable a tape library or drive in DPM to perform maintenance or repairs. You can reenable it as follows:

1.  In DPM Administrator Console, go to the **Management** > **Libraries**. Select the tape library or drive and enable or disable it.

## <a name="BKMK_Detect"></a>Detect tape drives
DPM automatically detects a tape library or drive that’s physically attached to the DPM server, and displays information in the **Libraries** If the tape library or drive isn’t displayed do the following:

1.  In the **Libraries** workspace click **Rescan**.

2.  If settings aren’t correct try remapping the tape drive.

## <a name="BKMK_Rename"></a>Rename a tape library
You can assign a new name to a tape library or drive as follows:

1.  In the **Libraries** workspace, select the tape library or drive > **Rename library**. Specify a new name and click **Rename**. The new name only appears in the DPM Administrator Console.

## <a name="BKMK_Lock"></a>Lock or unlock a library door
If your tape library does not have an insert\/eject \(I\/E\) port, you can use the following procedures to lock or unlock the tape library door”

1.  On the **Libraries** tab, select the library and click **Lock library door** or **Unlock library door**.

## <a name="BKMK_Clean"></a>Clean a tape drive
To clean a drive in a tape library, you must specify which tape to use for cleaning, and then start the cleaning job. If a cleaning tape is online and marked as a cleaning tape, you only need to run the cleaning job.

1.  In the**Libraries** workspace select the drive and click **Clean drive**.

## Windows PowerShell instructions

#### To enable a library using DPM Management Shell

-   Use the following syntax to retrieve the library:

    **Get\-DPMLibrary \[\-DPMServerName\]** *<String>* **\[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to enable a library:

    **Enable\-DPMLibrary \[\-DPMLibrary\]** *<Library\[\]>* **\[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Enable\-DPMLibrary \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Enable\-DPMLibrary \-full**" in DPM Management Shell.

#### To disable a library using DPM Management Shell

-   Use the following syntax to retrieve the library:

    **Get\-DPMLibrary \[\-DPMServerName\]** *<String>* **\[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to disable a library:

    **Disable\-DPMLibrary \[\-DPMLibrary\]** *<Library\[\]>* **\[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\] \[\-WhatIf\] \[\-Confirm\]**

    For more information, type "**Get\-Help Disable\-DPMLibrary \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Disable\-DPMLibrary \-full**" in DPM Management Shell.

#### To rename a tape library using DPM Management Shell

-   Use the following syntax to retrieve the library:

    **Get\-DPMLibrary \[\-DPMServerName\]** *<String>* **\[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to rename the library:

    **Rename\-DPMLibrary \[\-DPMLibrary\]** *<Library>* **\[\-NewName\]** *<String>* **\[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Rename\-DPMLibrary \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Rename\-DPMLibrary \-full**" in DPM Management Shell.

#### To lock a tape library door using DPM Management Shell

-   Use the following syntax to unlock a library door:

    **Lock\-DPMLibraryDoor \[\-DPMLibrary\]** *<Library>* **\[\-Async\] \[\-DoorAccessJobStateChangeEventHandler** *<DoorAccessJobStateChangeEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Lock\-DPMLibraryDoor \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Lock\-DPMLibraryDoor \-full**" in DPM Management Shell.

#### To unlock a tape library door using DPM Management Shell

-   Use the following syntax to unlock a library door:

    **Unlock\-DPMLibraryDoor \[\-DPMLibrary\]** *<Library>* **\[\[\-Timeout\]** *<Int32>***\] \[\-Async\] \[\-DoorAccessJobStateChangeEventHandler** *<DoorAccessJobStateChangeEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Unlock\-DPMLibraryDoor \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Unlock\-DPMLibraryDoor \-full**" in DPM Management Shell.

#### To clean a tape drive using DPM Management Shell

-   Use the following syntax to retrieve a tape drive:

    **Get\-DPMTapeDrive \[\-DPMLibrary\]** *<Library\[\]>* **\[\-Verbose\] \[\-Debug\]\[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\]\[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to clean a drive:

    **Start\-DPMTapeDriveCleaning \[\-TapeDrive\]** *<Drive\[\]>* **\[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\]\[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\]\[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Start\-DPMTapeDriveCleaning \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Start\-DPMTapeDriveCleaning \-full**" in DPM Management Shell.


