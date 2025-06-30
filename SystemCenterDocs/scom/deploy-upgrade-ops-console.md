---
ms.assetid: 89b1617f-73d3-4a5d-9a82-3ef4ab1a9fc3
title: Upgrade an Operations Console
description: This article describes how to upgrade an Operations console to the latest version of System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency.5, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade an Operations console



This procedure upgrades a standalone Operations console to System Center - Operations Manager. Perform this procedure locally on the computer that has a standalone Operations console installed. You don't have to perform this procedure to upgrade Operations consoles that are installed locally on a management server.

Before you begin the upgrade process, ensure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

## Upgrade a standalone Operations console

1. Sign in to the computer that hosts the Operations console with an account that is a member of the Operations Manager Administrators role in your Operations Manager management group.

2. On the Operations Manager source media, run **Setup.exe**, and select **Install**.

    > [!NOTE]
    > The **Getting Started** page displays information about what will be upgraded. Select **Next** to proceed with the upgrade.

3. On the **Getting Started, Please read the license terms page**, read the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and select **Next**.

4. On the **Select installation location** page, accept the default value, enter a new location, or browse to one. Then select **Next**.

::: moniker range="sc-om-2016"
   > [!NOTE]
   > The default path is C:\Program Files\Microsoft System Center 2016\Operations Manager. 
::: moniker-end

::: moniker range=">sc-om-2016"
   > [!NOTE]
   > The default path is C:\Program Files\Microsoft System Center\Operations Manager.
::: moniker-end

5. On the **Prerequisites** page, review and address any warnings or errors that are returned by the Prerequisites checker, and select **Verify Prerequisites Again** to recheck the system.

6. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration**, **Ready To Upgrade** page, select **Upgrade**.

8. When the upgrade is finished, the **Upgrade complete** page appears. Select **Close**.

### Upgrade a stand-alone Operations console from the Command Prompt

1. Sign in to the computer that hosts the Operations console with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group.

2. Open an elevated Command Prompt by using the **Run as Administrator** option.

3.  Change to the path to the Operations Manager source media, and run the following command.

    ```
    Setup.exe /silent / upgrade /AcceptEndUserLicenseAgreement:1
    ```

### Verify the Operations console upgrade

1. On the Windows desktop, select **Start**, and select **Run**.

2. Enter **regedit**, and select **OK**. The Registry Editor starts.

    > [!CAUTION]
    > Incorrectly editing the registry can severely damage your system. Before you make changes to the registry, you should back up any valued data that is on the computer.

3. Browse to the **HKey_Local_Machine\Software\Microsoft\Microsoft Operations Manager\3.0\Setup** key.

::: moniker range="sc-om-2016"
The value of the **UIVersion** entry is 7.2.11719.0.
::: moniker-end




## Next steps

- After you've upgraded all of the standalone operations consoles in your management group, you can upgrade the agents. For more information, see [How to Upgrade an Agent to System Center Operations Manager](~/scom/deploy-upgrade-agents.md).

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
