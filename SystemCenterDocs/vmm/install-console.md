---
ms.assetid: 857ab713-df3e-4744-aac9-e057efc0fce7
title: Install the VMM console
description: This article provides installation instructions for the VMM console
author: jyothisuri
ms.author: jsuri
ms.date: 06/04/2025
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency.5, intro-installation, engagement-fy24
---

# Install the VMM Console

This article describes how to install the System Center Virtual Machine Manager (VMM) console on a remote computer and connect to the VMM server. When you install the VMM management server, the console is installed on it automatically.

>[!NOTE]
>The default timeout value for a VMM client session is 330 seconds, and it's specific to each client. To update the timeout value, create *IndigoSendTimeout* registry in all the client machines from where the timeout needs to be configured. The registry is located at **Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Administrator Console\Settings**.
>
>The registry is of type DWORD (32-bit), the minimum value is 330 seconds, and the maximum is 900 seconds (15 minutes).


## Before you start

- Check the supported operating systems for the console that are detailed in the system requirements.
- Review and ensure you meet the system requirements. [Learn about](system-requirements.md) system requirements.
- Ensure that you have at least local administrator permissions on the computer on which you're installing the console.
::: moniker range="<=sc-vmm-2019"
- The VMM version of the console must match the System Center version of the VMM server. For example, to connect to a VMM server running System Center 2016, the VMM console version must also be 2016.
::: moniker-end
::: moniker range="sc-vmm-2022"
- The VMM version of the console must match the System Center version of the VMM server. For example, to connect to a VMM server running System Center 2022, the VMM console version must also be 2022.
::: moniker-end
::: moniker range="sc-vmm-2025"
- The VMM version of the console must match the System Center version of the VMM server. For example, to connect to a VMM server running System Center 2025, the VMM console version must also be 2025.
::: moniker-end
- You can only install one version of the console on a single machine.
::: moniker range="sc-vmm-2025"
- The VMM Console is installed using the same installer as the VMM server. Ensure you have the installer downloaded from one of the [procurement channels](/system-center/vmm/install?view=sc-vmm-2025&preserve-view=true#before-you-start).
::: moniker-end
::: moniker range="sc-vmm-2022"
- The VMM Console is installed using the same installer as the VMM server. Ensure you have the installer downloaded from one of the [procurement channels](/system-center/vmm/install?view=sc-vmm-2022&preserve-view=true#before-you-start).
::: moniker-end

::: moniker range=">=sc-vmm-2019"

[!INCLUDE [validation-virtual-machine-manager.md](../includes/validation-virtual-machine-manager.md)]

::: moniker-end

## Run setup

1. Review the planning instructions. Then, right-click setup.exe for VMM > **Run as administrator**.
2. On the main setup page, select **Install** and on the **Select features to install** page, select the **VMM console** checkbox, and then select **Next**. On the **Please read this notice page**, select the **I agree with the terms of this notice** checkbox, and then select **Next**.
3. Review the information on the **Diagnostic and Usage Data** page, and then select **Next**. On the **Microsoft Update** page, select whether you want to use Microsoft Update, and then select **Next**. This page won't appear if updates are already installed.
4. On the **Installation location** page, enter an installation path for the VMM program files or use the default path, and then select **Next**. Set up checks that the computer meets the console installation requirements.
5. On the **Port configuration** page, enter the port that you want to use for the VMM console to communicate with the VMM management server, and then select **Next**. The port setting that you assign for the VMM console should match the port setting that you assigned for the VMM console during the installation of the VMM management server. The default port setting is 8100. Also, don't assign port number 5986 because it's preassigned.
6. On the **Installation summary** page, review the settings and select **Install**. The **Installing features** page appears and displays the installation progress.
7. On the **Setup completed successfully** page, select **Close** to finish the installation. Select **Open the VMM console when this wizard closes** to open the console after the wizard finishes. If setup doesn't finish successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

If you want to uninstall the console, do the following:

1. In the Control Panel, select to uninstall a program and select Microsoft System Center Virtual Machine Manager.
2. In **Select features to remove**, select **VMM console**. On the VMM management server, you can't uninstall the console without uninstalling VMM management.
3. In **Summary**, review the settings and select **Uninstall**.

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
3. Run setup as follows: setup.exe /client /i /IACCEPTSCEULA /f \<path\>, where:
   - /client - specifies console installation
   - /i or /x - specify whether to install (/i) or uninstall (/x) the console.
   - /IACCEPTSCEULA - Specifies that you have read, understood, and accepted the terms of use.
   - /f &lt;filename&gt; - specifies the ini file to use. Make sure this is correct. If setup doesn't find the ini file, it installs with default values.
   - path: location of ini file.
   - Don't use the /opsmgr parameter

Example: **setup.exe /client /i /IACCEPTSCEULA /f C:\Temp\VMClient.ini**.

## Connect to a VMM management server

1. On the remote machine desktop, select the VMM console icon if the console isn't open.
2. Specify the server name and port on which the VMM server is listening (8100 by default). For example, **vmmserver01:8100**.
3. You can use the account with which you're signed in to the remote machine or specify a different account to connect to VMM. Select **Automatically connect with these settings** if you want to connect to the same VMM server each time.
4. Select **Connect**. **Select User Role** appears if the credentials you're using belong to more than one VMM user roles.
