---
title: Manage tapes in the DPM library
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a122cc9a-ce88-4a3a-9c17-f48b482dc0f7
---
# Manage tapes in the DPM library
Use the following procedures to manage tapes in the library:

-   [Add to remove tapes](#BKMK_Add)

-   [Inventory tapes](#BKMK_In)

-   [Mark a tape as free](#BKMK_Free)

-   [Identify an unknown tape](#BKMK_Identify)

-   [Recatalog an imported tape](#BKMK_Recat)

-   [View tape contents](#BKMK_ViewContents)

-   [Mark a tape as a cleaning tape](#BKMK_Clean)

-   [Erase a tape](#BKMK_Erase)

## <a name="BKMK_Add"></a>Add or remove tapes
You can add or remove tapes from the tape library. For standalone tape drives follow the manufacturer’s instructions for adding or removing tapes. Add or remove tapes as follows:

1.  Physically add the tape to the I\/E port of the tape library.

2.  In DPM Administrator Console, go to the **Management** view, and then open the **Libraries** workspace.

3.  In the **Actions** pane, click **Add tape \(I\/E port\)** . DPM performs a fast inventory on the tape library and adds tapes into the free slots available in the tape library. This enables you to add tapes into the I\/E port which remains open for a time period of 10 minutes. If sufficient numbers of slots are not free then the tapes are left in the I\/E Port and the Add tape \(I\/E port\) operation fails.

    Note htat if you add or remove tapes to the tape library using **Unlock library door** or **Add tape**, DPM will automatically inventory the library. If you add or remove tapes to the tape library without using **Unlock library door** or **Add tape**, you must use the **Inventory library** action to the DPM Administrator Console.

#### To add a tape by using DPM Management Shell

-   Use the following syntax to add a tape using the I\/E port:

    **Lock\-DPMLibraryIEPort \[\-DPMLibrary\]** *<Library>* **\[\-Async\] \[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Lock\-DPMLibraryIEPort \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Lock\-DPMLibraryIEPort \-full**" in DPM Management Shell.

#### To remove a tape by using the I\/E port

1.  In DPM Administrator Console, go to the **Management** view, and then open the **Libraries** workspace.

2.  In the display pane, expand the tape library from which you want to remove a tape.

3.  Expand **Slots**, and then select the slot that holds the tape to be removed.

4.  Click **Remove tape**.

5.  Physically remove the tape from the I\/E port of the tape library.

#### To remove a tape by using DPM Management Shell

-   Use the following syntax to add a tape using the I\/E port:

    **Unlock\-DPMLibraryIEPort \[\-DPMLibrary\]** *<Library>* **\[\-Async\] \[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Unlock\-DPMLibraryIEPort \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Unlock\-DPMLibraryIEPort \-full**" in DPM Management Shell.

## <a name="BKMK_In"></a>Inventory tapes
You can inventory tapes by performing a fast inventory that reads the barcode of each tape in the library \(when the tape has a barcode and the library has a barcode reader\), or a detailed inventory that reads the header area of a tape to identify the on\-media ID \(OMID\) on each tape. Run an inventory as follows:

1.  In the DPM Administrator Console click **Management** > **Libraries** and then select a library.

2.  Click **Inventory** > **Fast inventory** or **Detailed inventory**> **Start**.

## <a name="BKMK_Free"></a>Mark a tape as free
A *free* tape is a tape that blank or available to be written to by operations such as backup or copy. To reuse an expired tape from another server you add it to tape library or drive and mark it as free. Expired tapes that are being managed by that [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server can be reused automatically without marking. Mark a tape as follows:

1.  In the DPM Administrator Console click **Management** > **Libraries** and then select a library.

2.  Select a tape and **Mark as free**.

#### To mark a tape as free using DPM Management Shell

-   Use the following syntax to mark a tape as free:

    **Set\-Tape \[\-Tape\]** *<Media\[\]>* **\-Free \[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

-   Use the following syntax to mark a tape as not free:

    **Set\-Tape \[\-Tape\]** *<Media\[\]>* **\-NotFree \[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Set\-Tape \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Set\-Tape \-full**" in DPM Management Shell.

#### To mark a tape containing valid data sets as free

1.  Open a new Notepad file, and then copy the following script into it:

    ```
    param ([string] $DPMServerName, [string] $LibraryName, [string[]] $TapeLocationList)

    if(("-?","-help") -contains $args[0])
    {
        Write-Host "Usage: ForceFree-Tape.ps1 [[-DPMServerName] <Name of the DPM server>] [-LibraryName] <Name of the library> [-TapeLocationList] <Array of tape locations>"
        Write-Host "Example: Force-FreeTape.ps1 -LibraryName "My library" -TapeLocationList Slot-1, Slot-7"
        exit 0
    }

    if (!$DPMServerName)
    {
        $DPMServerName = Read-Host "DPM server name: "

        if (!$DPMServerName)
        {
            Write-Error "Dpm server name not specified."
            exit 1
        }
    }

    if (!$LibraryName)
    {
        $LibraryName = Read-Host "Library name: "

        if (!$LibraryName)
        {
            Write-Error "Library name not specified."
            exit 1
        }
    }

    if (!$TapeLocationList)
    {
        $TapeLocationList = Read-Host "Tape location: "

        if (!$TapeLocationList)
        {
            Write-Error "Tape location not specified."
            exit 1
        }
    }

    if (!(Connect-DPMServer $DPMServerName))
    {
        Write-Error "Failed to connect To DPM server $DPMServerName"
        exit 1
    }

    $library = Get-DPMLibrary $DPMServerName | where {$_.UserFriendlyName -eq $LibraryName}

    if (!$library)
    {
        Write-Error "Failed to find library with user friendly name $LibraryName"
        exit 1
    }

    foreach ($media in @(Get-Tape -DPMLibrary $library))
    {
        if ($TapeLocationList -contains $media.Location)
        {
            if ($media -is [Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.LibraryManagement.ArchiveMedia])   
            {
                foreach ($rp in @(Get-RecoveryPoint -Tape $media))
                {
                    Get-RecoveryPoint -Datasource $rp.Datasource | Out-Null

                    Write-Verbose "Removing recovery point created at $($rp.RepresentedPointInTime) for tape in $($media.Location)."
                    Remove-RecoveryPoint -RecoveryPoint $rp -ForceDeletion -Confirm:$false
                }

                Write-Verbose "Setting tape in $($media.Location) as free."
                Set-Tape -Tape $media -Free
            }
            else
            {
                Write-Error "The tape in $($media.Location) is a cleaner tape."
            }
        }
    }

    ```

2.  Save the file as ForceFree.ps1.

3.  The syntax to run the script is ForceFree.ps1 \-DPMServerName <Name of server> \-LibraryName <Name of library> \-TapeLocation <slot numbers>.

## <a name="BKMK_Identify"></a>Identify an unknown tape
When a data tape displays as "Unknown", you can use DPM to identify it by reading the tape header and updates the tape label as follows:

-   A tape created by the DPM server displays the assigned tape label.

-   A tape created by another DPM server displays **Imported** as the tape label.

-   A tape that contains content that was not created by DPM displays **Unrecognized** as the tape label.

-   A tape that has conflicting identification information, such as the bar code or the on\-media identifier, displays **Suspect** as the tape label.

Identify an unknown tape as follows:

1.  In the DPM Administrator Console click **Management** > **Libraries** and then select a library.

2.  Select the unknown tape > **Identify unknown tape**.

## <a name="BKMK_Recat"></a>Recatalog an imported tape
An *imported tape* contains content that was created by another DPM server. When you add it to the tape library you’ll need to recatalog it to identify the contents. During the recatalog, DPM reads from the tape and adds information about the data that it contains to the database. After recatalog completes, you can recover data from the tape by selecting a recovery point from the data on the tape. Import as follows:

1.  In the DPM Administrator Console click **Management** > **Libraries**. Select the tape to import and click **Recatalog imported tape**.

    If you try to recatalog a tape in a shared library from a DPM server other than the one from which the backup was taken, you will not see the **Recatalog** and **View Contents** options in the tool ribbon. 
    Run a detailed inventory on that tape. After the inventory is completed, the **Recatalog** and **View Contents** options are enabled on the tool ribbon.

#### To recatalog an imported tape using DPM Management Shell

-   Use the following syntax to recatalog an imported tape:

    **Start\-TapeRecatalog \[\-Tape\]** *<Media\[\]>* **\[\-JobStateChangedEventHandler** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Start\-TapeRecatalog \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Start\-TapeRecatalog \-full**" in DPM Management Shell.

## <a name="BKMK_ViewContents"></a>View tape contents
You can view the contents of a tape, and copy the data that is on the tape to disk.

1.  In the DPM Administrator Console click **Management** > **Libraries** and then select a library.

2.  Select the tape and click **View tape contents**.

## <a name="BKMK_Clean"></a>Mark a tape as a cleaning tape
To clean a drive in a tape library using DPM, you specify which tape to use for cleaning, and then start the cleaning job.

If the barcode on a tape starts with "CLN" \(for example, bar code CLN0000812\), DPM identifies the tape as a cleaning tape after a fast inventory. If it doesn’t \(or the barcode doesn’t start with "CLN", you must mark the tape as a cleaning tape and then run a detailed inventory. If you don’t, a cleaning job will start when DPM mounts this tape during the detailed inventory. Mark the tape as follows:

1.  In the DPM Administrator Console click **Management** > **Libraries**.

2.  Select the tape and **Mark as cleaning tape**.

3.  In **Inventory** > **Detailed inventory**, click **Start**.

#### To mark a tape as a cleaning tape using DPM Management Shell

-   Use the following syntax to mark a tape as a cleaning tape:

    **Set\-Tape \[\-Tape\]** *<Media\[\]>* **\-Cleaner \[\-PassThru\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction** *<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable** *<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Set\-Tape \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Set\-Tape \-full**" in DPM Management Shell.

## <a name="BKMK_Erase"></a>Erase a tape
You can reuse an expired tape without erasing the contents of the tape. However, you can erase a tape to remove sensitive or critical information as follows:

1.  In the DPM Administrator Console click **Management** > **Libraries**.

2.  Select the tape > **Erase tape**.

#### To erase a tape using DPM Management Shell

-   Use the following syntax to erase a tape:

    **Start\-TapeErase \[\-Tape\]** *<Media\[\]>* **\[\[\-JobStateChangeHandler\]** *<JobStateChangedEventHandler>***\] \[\-Verbose\] \[\-Debug\] \[\-ErrorAction***<ActionPreference>***\] \[\-ErrorVariable** *<String>***\] \[\-OutVariable***<String>***\] \[\-OutBuffer** *<Int32>***\]**

    For more information, type "**Get\-Help Start\-TapeErase \-detailed**" in DPM Management Shell.

    For technical information, type "**Get\-Help Start\-TapeErase \-full**" in DPM Management Shell.

### Enable short erase
By default, when you erase a tape by using [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)], it performs a long erase. If your tape drive supports short erase, you can enable it on the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server by creating the DWORD **UseShortErase** under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Agent`.

Set the value of the DWORD to 00000000.

After this value is set, all erase operations on the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server will be short erases. To revert to long erases, remove this registry key.

Short erase is faster but it doesn’t erase the data.. If you have a policy that all data from the tape must be erased and unrecoverable you shouldn’t use this option.

