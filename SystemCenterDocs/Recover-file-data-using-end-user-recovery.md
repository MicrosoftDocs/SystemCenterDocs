---
title: Recover file data using end-user recovery
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b79610f-a0dd-4388-b85e-7274edf65e6e
---
# Recover file data using end-user recovery
After users install the recovery point client, they can recover previous versions of data by retrieving recovery points from server for [!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)]. For more information, see [How to Install the Shadow Copy Client Software \[DPM2012\_Web\]](assetId:///6cb51208-648a-4cde-b390-2a2859d51292).

> [!NOTE]
> If a user recovers data using Microsoft Word on a Windows Server 2008 operating system, there is no need to install the shadow copy client software.

If a protected file was created in an application that supports recovering previous versions of data, you can recover the file by using the application in which it was created.

### To recover data by using a client computer

1.  Click **Start**, click **Run**, and type the path to the protected data.

2.  Browse to the file, right\-click the file name, and then click **Properties**.

3.  On the **Properties** menu, click **Previous Versions**, and then select the version that you want to recover from the list of available versions.

### To recover data by using applications in Office 2003 or later on a client computer running Windows Server 2000 or Windows 2003

1.  Open the application in which the data was created.

    > [!NOTE]
    > Applications in Office 2003 or later, such as Word 2003 and Excel 2003, support recovery of previous versions.

2.  On the **File** menu, click **Open**.

3.  In the **Tools** drop\-down list, click **Properties**, click **Previous Versions**, and then select the version you want to recover from the list of available versions.

    > [!NOTE]
    > When the user browses for recoverable data, the shadow copy client first checks for local recovery points on the protected computer. If local recovery points are available, a list of existing recovery points on the protected computer is displayed. If no recovery points are available on the protected computer, a list of existing recovery points on the DPM server is displayed.

### To recover data by using Microsoft Word 2007 on a client computer running Windows Vista or Windows XP

1.  Open the application in which the data was created.

    > [!NOTE]
    > This procedure assumes that you selected to have Microsoft Word 2007 make backup copies.

2.  Click **Microsoft Office**, and then click **Open**.

3.  In the box next to the **File name** box on a computer that is running Windows Vista, or in the **Files of type** box on a computer that is running Windows XP, click **All Files**.

4.  If you want to open a backup copy that was saved in a different folder, locate and open the folder.

5.  Click the arrow next to **Views**, and then click **Details**. In the **Name** column, the backup copy name appears as **Backup of <document name>**. In the **Type** column, the file type for the backup copy appears as **Microsoft Word Backup Document**.

6.  Locate and double\-click the backup copy to open it.

7.  If you want to work with the backup copy as a regular Word document, click **Microsoft Office**, click **Save As**, and then type a name for the file in the **File name** box.

## See Also
[How to Disable End\-User Recovery \[DPM2012\_Web\]](assetId:///8aeb84d9-ce40-4830-bc93-158e06837854)
[How to Enable End\-User Recovery \[DPM2012\_Web\]](assetId:///f0588d9e-aa2e-45f2-94cb-604b6f381812)
[How to Install the Shadow Copy Client Software \[DPM2012\_Web\]](assetId:///6cb51208-648a-4cde-b390-2a2859d51292)


