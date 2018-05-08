---
ms.assetid: 857ab713-df3e-4744-aac9-e057efc0fce7
title: Install the VMM console
description: This article provides installation instructions for the VMM console
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  05/06/2018
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Install the VMM Console

This article describes how to install the System Center Virtual Machine Manager (VMM) console on a remote computer, and connect to the VMM server. When you install the VMM management server, the console is installed on it automatically.


## Before you start

- Check the supported operating systems for the console that are detailed in the system requirements.
- Review and ensure you meet the system requirements. Learn about [system requirements 2016](system-reqs.md) and [system requirements 1801](system-reqs-1801.md).
- Make sure you have at least local administrator permissions on the computer on which you're installing the console.
- The VMM version of the console must match the System Center version of the VMM server. For example, to connect to a VMM server running System Center 2016, the VMM console version must also be 2016.
- You can only install one version of the console on a single machine.

## Run setup

1. Review the planning instructions. Then, right-click setup.exe for VMM > **Run as administrator**.
1. On the main setup page, click **Install** and on the **Select features to install** page, select the **VMM console** check box, and then click **Next**. On the **Please read this notice page**, select the **I agree with the terms of this notice** check box, and then click **Next**.
1. Review the information on the **Diagnostic and Usage Data** page, and then click **Next**. On the **Microsoft Update** page, select whether you want to use Microsoft Update, and then click **Next**. This page won't appear if updates are already installed.
1. On the **Installation location** page, type an installation path for the VMM program files or use the default path, and then click **Next**. Setup checks that the computer meets the console installation requirements.
1. On the **Port configuration** page, type the port that you want to use for the VMM console to communicate with the VMM management server, and then click **Next**. The port setting that you assign for the VMM console should match the port setting that you assigned for the VMM console during the installation of the VMM management server. The default port setting is 8100. Also, do not assign port number 5986, because it is preassigned.
1. On the **Installation summary** page, review the settings and click **Install**. The **Installing features** page appears and displays the installation progress.
1. On the **Setup completed successfully** page, click **Close** to finish the installation. Select **Open the VMM console when this wizard closes** to open the console after the wizard finishes. If setup does not finish successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

If you want to uninstall the console do the following:

1. In the Control Panel click to uninstall a program and select Microsoft System Center Virtual Machine Manager.
2. In **Select features to remove** click **VMM console**. On the VMM management server, you can't uninstall the console without uninstalling VMM management.
3. In **Summary** review the settings and click **Uninstall**.

## Install the console from the command prompt

You can install the VMM administrator console from the command line by using the VMClient.ini file to customize the installation options. You can set the parameters as follows:

**Parameter** | **Value**
--- | ---
ProgramFiles | Specify the location in which to store program files.
IndigoTCpPort | Specify the port number used to communicate with the VMM server.
MUOptIn | 0: Don't opt in to Microsoft Update. 1: Opt in.
VmmServerForOpsMgrConfig | Specify the name of the System Center Operations Manager server.

Install the console as follows:


1. Copy the VMClient.ini file from the amd64\Setup folder to a local folder.
2. Edit the VMClient.ini file. Remove the comment indicator (#) only if you want to edit the entry. Otherwise, setup uses the values in the .ini file as the default values.
3. Run setup as follows: setup.exe /client /i /f <path>, where:
    - /client - specifies console installation
    - /i or /x - specify whether to install (/i) or uninstall (/x) the console.
    - /f &lt;filename&gt; - specifies the ini file to use. Make sure this is correct. If setup doesn't find the ini file, it installs with default values.
    - <path> - location of ini file.
    - Don't use the /opsmgr parameter

Example: **setup.exe /client /i /f C:\Temp\VMClient.ini**.

## Connect to a VMM management server

1. On the remote machine desktop click the VMM console icon if the console isn't open.
1. Specify the server name and port on which the VMM server is listening (8100 by default). For example: **vmmserver01:8100**.
1. You can use the account with which you're logged on to the remote machine or specify a different account to connect to VMM. Click **Automatically connect with these settings** if you want to connect to the same VMM server each time.
1. Click **Connect**. **Select User Role** appears if the credentials you're using belong to more than one VMM user role.
