---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system center 2016
keywords:  system center, dpm
ms.date:  2016-06-17
title:  Identify compatible tape libraries
ms.technology:  dpm
---

---
title: Identify compatible tape libraries
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ed6e64f-21d4-4c93-9979-3f1a48317cbe
---
# Identify compatible tape libraries
Use the TechNet wiki to find the latest list of [compatible tape libraries for DPM](http://social.technet.microsoft.com/wiki/contents/articles/17105.compatible-tape-libraries-for-system-center-2012-dpm.aspx).

## Virtual tape library support
Virtual tape libraries configured with a virtual fibre channel adapter are supported if you’re running Data Protection Manager 2012 R2 UR3 or later with certified hardware listed in the wiki. To check if your tape library is supported by the virtual fibre channel adapter, ask your tape hardware vendor to verify tape library compatibility.

## Verify tape library compatibility
If the tape is listed in the [Windows Server Catalog](http://www.windowsservercatalog.com/) in the Hardware, Storage section, and is shown as compatible with Windows 2008 64\-bit, or Windows 2008 R2 64\-bit \- it will probably work with DPM. Note that any driver incompatibilities with Windows 2012 would need to be addressed by the vendor.
If you already have a tape you can run the DPM Tape Library Compatibility Test tool as described below.

## Run the compatibility tool
Before you run the tool, do the following:

-   Check your target tape library and tape drives are visible in Device Manager.

-   Insert a read\/write data tape in slot 0. The contents of this tape will be overwritten.

-   Insert a cleaning tape in slot 1. The tapes must be in consecutive slots, failing which there should be no tapes in the slots between the tapes. The data tape is in a slot preceding the cleaning tape.

1.  Download the [DPM Tape Library Compatibility Test Tool](http://go.microsoft.com/fwlink/?LinkId=203337).

2.  Extract the files. Open an elevated command prompt, and navigate to the folder to which you extracted the tool.

3.  To check that the tape is visible to the tool, type **DPMLibraryTest.exe \/CERTIFY \/LL.** . Then certify as follows:

    -   To certify a tape library, type D**PMLibraryTest.exe \/CERTIFY \/TL <tape library name> \/AT**

    -   To certify a standalone tape drive, type D**PMLibraryTest.exe \/CERTIFY \/TL <device name> \/SA**

4.  The tool runs the following tests:

    -   **Test 1: Basic configuration**—Scans the system for attached devices, and identifies standalone tape drives and tape libraries. The tool provides a summary at the end of the test. For each device you’ll see a Device Name, Serial Number, Vendor Name, Product Name, Firmware Revision, and SCSI properties. You should verify that the summary information is correct. If it isn’t:

        -   Check all devices are listed in Device Manager.

        -   Ensure that device drivers are up\-to\-date.

        -   .If the drive mappings are incorrect, use the DPMDriveMapping.exe tool in the <DPM installation folder>\/bin folder to correct the mappings. If you don’t have DPM installed on the computer, copy the DPMLA.xml that DPMDriveMapping.exe creates to the folder to which you extracted the Tape Library Certification tool.

    -   **Test 2: Mount\/dismount**—This test selects a tape from the first available slot and performs a mount\/\/\/dismount of the tape to and from a drive.

    -   **Test 3: Drive cleaning**—This test performs a cleaning test using the cleaning tape. If you are using Firestreamer to a VTL where you can’t remove or change tapes, use the \/ST flag syntax to skip this test.

    -   **Test 4: I\/E media**—This test selects the first available tape and moves it to the I\/E port and back. If your library\/VTL doesn’t have I\/E ports, the tool will automatically skip the test.

    -   **Test 5: I\/O**—This test selects the first writable tape, writes a few buffers to it, and then attempts to read what’s been written. This test only checks read\/write capabilities. Any specific errors in the drive should be inspected using the advanced mode.

5.  After the tool completes the test, log information will be provided in the LibraryTestTool\-\*Curr.errlog files which are located in the folder from which you ran the tool. If the tests complete successful you can assume your tape library should work with DPM.

## Run the compatibility tool for Hyper\-V fiber channel

-   Prepare two Hyper\-V hosts running DPM.

-   Enable live migration on both the servers. A clustered deployment isn’t required.
    3

-   Run the compatibility tool on the first host server, as described in the section above, and verify that tests complete successfully.

-   Initiate live migration to the second host server and wait for it to complete.
    5

-   .After DPM is running virtually on the second host server, run the compatibility tool on that host server, as described above, and verify that tests complete successfully. If the tests pass you can assume that the tape library will work with DPM.

## Examples
The tool syntax is:

```
DPMLibraryTest.exe /CERTIFY /<switch_1> [/switch_2]
```

|Switch|Details|Example|
|----------|-----------|-----------|
|\/LL|List avaialable tape libraries and drives|**DPMLibraryTest.exe \/CERTIFY \/LL**|
|\/LT|List all test cases||
|\/TL|Test a library||
|\/AT|Run all test cases|Run test on the physical library: **DPMLibraryTest.exe \/CERTIFY \/TL \\\\.\\Changer0 \/AT**|
|\/ST|Run specific tests|Run tests 3 and 4 on a physical library: **DPMLibraryTest.exe \/CERTIFY \/TL \\\\.\\Changer0 \/ST 3 4**<br /><br />Run all tests except cleaner: **DPMLibraryTest.exe \/CERTIFY \/TL \\\\.\\Changer0 \/ST 1 2 4 5**|
|\/SA|Run standalone drive test cases|**DPMLibraryTest.exe \/CERTIFY \/TL \\\\.\\Tape21745678 \/SA**|
|\/EX|Show examples||
|\/Help or \/?|Show help||

