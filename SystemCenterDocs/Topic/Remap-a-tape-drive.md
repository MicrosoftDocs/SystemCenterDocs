---
title: Remap a tape drive
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f622a8ae-c05b-48c4-b1be-e3ab6639c3d0
---
# Remap a tape drive
The **Rescan** action on the tool ribbon in the **Libraries** workspace of the **Management** view causes DPM to examine the tape drives that are attached to the DPM server and update the information displayed on the **Libraries** tab. The **Libraries** tab displays each stand\-alone tape drive, and each tape library and its drives.

When the physical state of the tape drives does not display correctly in DPM Administrator Console, you need to remap the tape drive information. For example, drives from a tape library are listed as stand\-alone tape drives, a drive for Library 1 is listed as belonging to Library 2, or a stand\-alone tape drive is reported as a drive within another library rather than as a stand\-alone tape drive.

> [!NOTE]
> If a tape drive is not mapped correctly, jobs that require the tape drive that is incorrectly mapped will fail.

You can either use the DPMDriveMapping.exe or manually create the DPMLA.xml to remap a tape drive.

## Remapping Tape Drive Using DPMDriveMapping.exe
To correct the tape drive mapping, you must create a file named DPMLA.xml with the correct information, and then click **Rescan**. You can create this file using DPMDriveMapping.exe from the *<DPM Install>*\\Bin folder.

Ensure the following before you run DPMDriveMapping.exe:

-   DPMLA service should not be running.

-   There should not be any tapes in the drive.

-   There should be at least one tape in each library which is not marked as Cleaner.

#### Procedure to Remap Tape Drive using DPMDriveMapping.exe

1.  Run DPMDriveMapping.exe from *<DPM Install>*\\Bin folder.

2.  Start the DPM Administrator Console.

3.  Click **Rescan**.

## Remapping Tape Drive Manually

#### Procedure to remap tape drive manually

1.  Create DPMLA.xml.

2.  Start DPM Administrator Console.

3.  Click **Rescan**.

### Creating DPMLA.xml
You can create the DPMLA.xml using the template provided with DPM.

##### Procedure to create DPMLA.xml

1.  Open LADriveRemappingTemplate.xml from Microsoft Data Protection Manager\\DPM\\Config in an XML editor or Notepad

2.  Follow the instructions in the template file

3.  Save the file as DPMLA.xml in the Microsoft Data Protection Manager\\DPM\\Config folder. You must save the file using the Unicode format.

> [!IMPORTANT]
> You should not make changes to LADriveRemappingTemplate.xml because future updates to DPM might include changes to the template file. If you modify LADriveRemappingTemplate.xml, updates to DPM cannot replace the template file.

The following is an example of the contents of a DPMLA.xml file that maps a drive that is reported as a stand\-alone tape drive into a library at the drive bay 0 in the library:

```
<?xml version="1.0" encoding="utf-16"?>
<LAConfig xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/2003/dls/LAConfig.xsd">
  <DriveReMapInfo IsMannuallyMapped="true"> 
    <DriveLibraryAssociation>
      <Drive SerialNumber="HUL4B06579" SCSIPort="10" SCSIBus="23" SCSITargetId="80" SCSILun="4" DriveBayIndex="0" />
      <Library SerialNumber="2B41146637" SCSIPort="6" SCSIBus="5" SCSITargetId="0" SCSILun="1" />
    </DriveLibraryAssociation>
  </DriveReMapInfo>
</LAConfig>
```

