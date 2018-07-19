---
ms.assetid: 
title:  How to upgrade to Operations Manager version 1807
description: This article describes how to perform an upgrade from System Center Operations Manager version 1801 to 1807.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 07/19/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1807'
ms.technology: operations-manager
ms.topic: article
---


# How to upgrade to Operations Manager version 1807
This article describes how to perform a successful upgrade of System Center Operations Manager version 1801 to 1807. For more information about this upgrade and what issues are addressed, see [KB4133779](https://support.microsoft.com/help/4133779). 

## Requirements 

This update is available from Microsoft Update in the following languages: 
- Chinese Simplified (CHS)
- Chinese Traditional (CHT)
- Czech (CSY)
- Dutch (NLD)
- English (ENU)
- French (FRA)
- German (DEU)
- Hungarian (HUN)
- Italian (ITA)
- Japanese (JPN)
- Korean (KOR)
- Polish (POL)
- Portuguese (Brazil) (PTB)
- Portuguese (Portugal) (PTG)
- Russian (RUS)
- Spanish (ESN)
- Swedish (SWE)
- Turkish (TUR)

Some components are multilanguage, and the updates for these components are not localized.

You must run this update as an administrator on the systems hosting the Operations Manager components and have System Administrator rights on the SQL Server instance hosting the Operations Manager databases and Reporting server role.

If you don't want to restart the computer after you apply the Operations console update, close the Operations console before you apply the update for the role.

Do not apply an update immediately after you install System Center Operations Manager version 1801. Wait several hours after deployment of a new management group before you apply any update.

If User Account Control is enabled, run the .msp update files from an elevated command prompt.


## Supported installation order

Install the update package in the following order:

1. Management group features:

   1. Management server or servers
   2. Audit Collection Services
   3. Web console server role computers
   4. Gateway server or servers
   5. Operations console role computers
   6. Reporting server

2. Apply SQL scripts.

3. Manually import the management packs.

4. Apply the Agent update to manually installed agents or approve for upgrade from the Pending Management view in the Operations console for agents discovered and installed from the console.

5. Apply the Nano Agent update to manually installed agent or approve the upgrade from the Pending view in the Operations console for agents discovered and installed from the console.

6. Update Unix/Linux management packs and agents.

## How to obtain Microsoft System Center Operations Manager 1807 Update
Update packages for Operations Manager are available from Microsoft Update or by manual download.

### Microsoft Update
To obtain and install an update package from Microsoft Update, follow these steps on a computer that has an Operations Manager component installed:

1.	Select **Start**, and then select **Control Panel**.

2.	In Control Panel, double-click **Windows Update**.

3.	In the Windows Update window, select **Check Online for updates from Microsoft Update**.

4.	Select **Important updates are available**.

5.	Select the update rollup package, and then select **OK**.

6.	Select **Install updates** to install the update package.

If your computer is running Windows Server 2016 or later, follow these steps:

1.	Select **Start**, and then select **Settings**.

2.	In Settings, select **Updates & Security**.

3.	On the **Windows Update** tab, select **Check Online for updates from Microsoft Update**.

4.	Select **Important updates are available**.

5.	Select the update rollup package, and then select **OK**.

6.	Select **Install updates** to install the update package.

### Manual download
Go to the following websites to manually download the update packages from the Microsoft Update Catalog:

   [Download the Operations Manager update package now](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=4133779).

## Update Operations Manager features

To download the update rollup package and extract the files that are contained in the update rollup package, follow these steps:

1. Download the update packages that Microsoft Update provides for each computer. Microsoft Update provides the appropriate updates according to the components that are installed on each computer. Or download from the Microsoft Update Catalog.
Apply the appropriate MSP files on each computer.

    >[!NOTE]
    >Windows Installer patch (.MSP file) files are included in the update package. Apply all patch packages that relate to a specific computer. For example, if the Web console and Operations console role is installed on a management server, apply the .MSP files on the management server. Apply one patch package to a server for each specific feature that is installed on the server.
    >

2. Execute the following SQL database SQL scripts on the SQL Server instance hosting the OperationsManagerDB database:

    `Update_rollup_mom_db.sql`

    >[!NOTE]This script is located in the following location: `%SystemDrive%\Program Files\Microsoft System Center\Operations Manager\Server\SQL Script for Update Rollups`

3. Import the following management packs: 

    * .mp

    For information about how to import a management pack from a disk, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).

    >[!NOTE]
    >Management packs are included in the Server component updates in the following location: `%SystemDrive%\Program Files\Microsoft System Center\Operations Manager\Server\Management Packs for Update Rollups`


## Update Nano Agent 

To manually install the updates to Nano Agent, download the [KB3209591-8.0.10913.0-NanoAgent.cab](https://www.microsoft.com/download/details.aspx?id=54790) file. You can install this update on a Nano Agent system by using the following PowerShell script:

```
.\UpdateNanoServerScomAgentOnline.ps1 -NanoServerFQDN <FQDN of target Nano Server> -BinaryFolder <Path where the update .cab is already expanded OR path to one or more Nano-agent update .cab files> -IsCabExpanded <$true if BinaryFolder path is to an expanded .cab, $false if it is for a packed .cab file(s)> -RemoveBackup <$true to remove the previous binaries from the agent machine>
```

>[!NOTE]
>The `UpdateNanoServerScomAgentOnline.ps1` file is available in the following location:`%SystemDrive%\Program Files\Microsoft System Center\Operations Manager\Server\AgentManagement\Nano\NanoServer`

## Update UNIX and Linux management packs

To install the updated monitoring packs and agents for UNIX and Linux operating systems, perform the following steps.

1. Apply System Center Operations Manager version 1807 Update to your System Center version 1801 Operations Manager management group.
2. Download the **Microsoft System Center 1801 MP for UNIX and Linux.msi** installer package file - [System Center Management Pack for UNIX and Linux Operating Systems](https://www.microsoft.com/download/details.aspx?id=29696)
3.	Install the management pack update package to extract the management pack files.
4.	Import the updated management pack for each version of Linux or UNIX that you are monitoring in your environment.
5.	Upgrade each agent to the latest version by using either the **Update-SCXAgent** Windows PowerShell cmdlet or the [UNIX/Linux Agent Upgrade Wizard](manage-upgrade-uninstall-crossplat-agent.md) from the Device Management node under the Administration workspace in the Operations console.  

