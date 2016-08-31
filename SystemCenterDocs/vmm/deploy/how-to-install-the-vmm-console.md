---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Install the VMM Console
ms.technology:  virtual-machine-manager
ms.assetid:  56f31a2e-68ec-49f0-b0e6-628c832897dc
---

# How to Install the VMM Console

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following procedure to install a VMM console.

To complete this procedure, you need, at a minimum, membership in the local Administrators group (or equivalent) on the computer that you are configuring.

### To install the VMM console

1.  To start the Virtual Machine Manager Setup Wizard, on your installation media, right-click **setup.exe**, and then click **Run as administrator**.

2.  On the main setup page, click **Install**.

3.  On the **Select features to install** page, select the **VMM console** check box, and then click **Next**.

4.  On the **Please read this notice page**, click **I agree with the terms of this notice**, and then click **Next**.

5.  Review the information on the **Customer Experience Improvement Program** page, and then click **Next**.

6.  On the **Microsoft Update** page, select whether you want to use Microsoft Update, and then click **Next**.

    > [!NOTE]
    > If you previously chose to use Microsoft Update on this computer, the **Microsoft Update** page does not appear.

7.  On the **Installation location** page, type an installation path for the VMM program files or use the default path, and then click **Next**.

    The setup program checks the computer on which you are installing the VMM console to ensure that the computer meets the appropriate hardware and software requirements. If your computer does not meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears.

    For information about hardware and software requirements for VMM, see [Preparing your environment for System Center 2016 - Virtual Machine Manager](Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

    If your computer meets all prerequisites, the **Port configuration** page appears.

8.  On the **Port configuration** page, type the port that you want to use for the VMM console to communicate with the VMM management server, and then click **Next**.

    > [!NOTE]
    > The port setting that you assign for the VMM console should match the port setting that you assigned for the VMM console during the installation of the VMM management server. The default port setting is 8100. Also, do not assign port number 5986, because it is preassigned.

9. On the **Installation summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to install the VMM console.

    After you click **Install**, the **Installing features** page appears and displays the installation progress.

10. On the **Setup completed successfully** page, click **Close** to finish the installation.

    To open the VMM console, ensure that the **Open the VMM console when this wizard closes** check box is selected.

> [!NOTE]
> If setup does not finish successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.



