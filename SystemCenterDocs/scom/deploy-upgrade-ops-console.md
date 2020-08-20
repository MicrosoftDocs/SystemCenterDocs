---
ms.assetid: 89b1617f-73d3-4a5d-9a82-3ef4ab1a9fc3
title: How to Upgrade an Operations Console
description: This article describes how to upgrade an Operations console to the latest version of System Center Operations Manager.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 01/15/2018
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade an Operations console

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

This procedure upgrades a stand-alone Operations console to System Center - Operations Manager. Perform this procedure locally on the computer that has a stand-alone Operations console installed. You do not have to perform this procedure to upgrade Operations consoles that are installed locally on a management server.

Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](plan-system-requirements.md).

## To upgrade a stand-alone Operations console

1.  Log on to the computer that hosts the Operations console with an account that is a member of the Operations Manager Administrators role in your Operations Manager management group.

2.  On the Operations Manager source media, run **Setup.exe**, and then click **Install**.

    > [!NOTE]
    > The **Getting Started** page displays information about what will be upgraded. Click **Next** to proceed with the upgrade.

3.  On the **Getting Started, Please read the license terms page**, read the Microsoft Software License Terms, click **I have read, understood, and agree with the license terms**, and then click **Next**.

4.  On the **Select installation location** page, accept the default value, type in a new location, or browse to one. Then click **Next**.

    > [!NOTE]
    > For System Center 2016 - Operations Manager, the default path is C:\Program Files\Microsoft System Center 2016\Operations Manager.  For current branch, the default path is C:\Program Files\Microsoft System Center\Operations Manager.
    >

5.  On the **Prerequisites** page, review and address any warnings or errors that are returned by the Prerequisites checker, and then click **Verify Prerequisites Again** to recheck the system.

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Ready To Upgrade** page, click **Upgrade**.

8.  When the upgrade is finished, the **Upgrade complete** page appears. Click **Close**.

### To upgrade a stand-alone Operations console from the Command Prompt

1.  Log on to the computer that hosts the Operations console with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group.

2.  Open an elevated Command Prompt by using the **Run as Administrator** option.

3.  Change to the path to the Operations Manager source media, and run the following command.

    ```
    Setup.exe /silent / upgrade /AcceptEndUserLicenseAgreement:1
    ```

### To verify the Operations console upgrade

1.  On the Windows desktop, click **Start**, and then click **Run**.

2.  Type **regedit**, and then click **OK**. The Registry Editor starts.

    > [!CAUTION]
    > Incorrectly editing the registry can severely damage your system. Before you make changes to the registry, you should back up any valued data that is on the computer.

3.  Browse to the **HKey_Local_Machine\Software\Microsoft\Microsoft Operations Manager\3.0\Setup** key. For System Center 2016 - Operations Manager, the value of the **UIVersion** entry is 7.2.11719.0.  For version 1801, the value of **UIVersion** is 8.0.13053.0.  


## Next steps

- After you have upgraded all of the stand-alone operations consoles in your management group, you can upgrade the agents.  See [How to Upgrade an Agent to System Center Operations Manager](~/scom/deploy-upgrade-agents.md) for more information.

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
