---
ms.assetid: ae000f5e-9d67-4d0d-b093-8d103dce2047
title: Upgrade a Reporting Server
description: This article describes how to upgrade the Reporting server to the latest version of System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.custom: UpdateFrequency.5, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade a Reporting server

::: moniker range=">=sc-om-2019"

Use this procedure to upgrade a standalone Reporting server to System Center Operations Manager. You shouldn't run upgrade on the Reporting server until after you've upgraded the management servers, gateways, Operation consoles, and agents.

Before you begin the upgrade process, ensure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

## Before you perform the upgrade

::: moniker-end

::: moniker range=">=sc-om-2019 <=sc-om-2022"

When you try to upgrade Reporting server to System Center Operations Manager 2019 Reporting server, the upgrade fails for the following configuration:

  * Server A is configured as the System Center 2016 - Operations Manager management server.
  * Server B is configured with SQL Server hosting the System Center Operations Manager 2019 operational and data  warehouse database, and Operations Manager Reporting server or a standalone SQL Server hosting Reporting server.

::: moniker-end

::: moniker range="sc-om-2025"

When you try to upgrade Reporting server to System Center Operations Manager 2025 Reporting server, the upgrade fails for the following configuration:

  * Server A is configured as the System Center 2022 - Operations Manager management server.
  * Server B is configured with SQL Server hosting the System Center Operations Manager 2022 operational and data  warehouse database, and Operations Manager Reporting server or a standalone SQL Server hosting Reporting server.

::: moniker-end
::: moniker range=">=sc-om-2019"

The prerequisites checker will report the following error:  **Management Server Upgraded Check - The management server to which this component reports has not been upgraded.**
::: moniker-end

::: moniker range=">=sc-om-2019 <=sc-om-2022"

To work around this issue, install the System Center 2016 - Operations Manager Operations console on the server hosting the Reporting server role and then retry upgrading the Reporting server role to version 2019. Once the upgrade is successfully completed, you can rerun setup and uninstall the upgraded Operations console from the Reporting server.  

::: moniker-end

::: moniker range="sc-om-2025"

To work around this issue, install the System Center 2022 - Operations Manager Operations console on the server hosting the Reporting server role and then retry upgrading the Reporting server role to version 2025. Once the upgrade is successfully completed, you can rerun setup and uninstall the upgraded Operations console from the Reporting server.  

::: moniker-end

## Upgrade the Reporting server

1. Sign in to the computer that hosts the Reporting server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group and the SQL Server sysadmin fixed server role.

2. On the Operations Manager source media, run **Setup.exe**, and select **Install**.

    > [!NOTE]
    > The **Getting Started** page displays information about what will be upgraded. Select **Next** to proceed with the upgrade.

3. On the **Getting Started, please read the license terms page**, read the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and then select **Next**.

4. On the **Select installation location** page, accept the default value, enter a new location, or browse to one. Then select **Next**.

    > [!NOTE]
    > The default path is C:\Program Files\Microsoft System Center\Operations Manager.

5. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify Prerequisites Again** to recheck the system.

6. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Ready to Upgrade** page, review the options, and select **Upgrade**.

8. When upgrade is finished, the **Upgrade complete** page appears. Select **Close**.

## Upgrade the Reporting server from the Command Prompt

1. Sign in to the computer that hosts the Reporting server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group.

2. Open an elevated Command Prompt by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager Setup.exe file is located, and run the following command:

    > [!NOTE]
    > If the Reporting server reports to an unsupported or inaccessible root management server, you must also pass the following parameter: `/ManagementServer: <ManagementServerName>`.

    ```
    setup.exe /silent /AcceptEndUserLicenseAgreement:1 /upgrade
    /ManagementServer: <ManagementServerName>

    ```

::: moniker range="sc-om-2016"

Use this procedure to upgrade a standalone Reporting server to System Center 2016 - Operations Manager. You shouldn't run upgrade on the Reporting server until after you've upgraded the management servers, gateways, Operation consoles, and agents.

Before you begin the upgrade process, ensure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

## Before performing the upgrade

When you try to upgrade System Center 2016 - Operations Manager Reporting server to System Center Operations Manager 2019 Reporting server, the upgrade fails for the following configuration:

* Server A is configured as the System Center 2016 - Operations Manager management server.
* Server B is configured with SQL Server hosting the System Center 2016 - Operations Manager operational and data warehouse database, and Operations Manager Reporting server or a standalone SQL Server hosting Reporting server.

The prerequisites checker will report the following error:  **Management Server Upgraded Check - The management server to which this component reports has not been upgraded.**

To work around this issue, install the System Center 2016 - Operations Manager Operations console on the server hosting the Reporting server role and then retry upgrading the Reporting server role to version 2019. Once the upgrade is successfully completed, you can rerun setup and uninstall the upgraded Operations console from the Reporting server.  

## To upgrade the Reporting server

1. Sign in to the computer that hosts the Reporting server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group and the SQL Server sysadmin fixed server role.

2. On the Operations Manager source media, run **Setup.exe**, and select **Install**.

    > [!NOTE]
    > The **Getting Started** page displays information about what will be upgraded. Select **Next** to proceed with the upgrade.

3. On the **Getting Started, Please read the license terms page**, read the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and then select **Next**.

4. On the **Select installation location** page, accept the default value, enter a new location, or browse to one. Then select **Next**.

    > [!NOTE]
    > For System Center 2016 - Operations Manager, the default path is C:\Program Files\Microsoft System Center 2016\Operations Manager.  For current branch, the default path is C:\Program Files\Microsoft System Center\Operations Manager.
    >

5. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify Prerequisites Again** to recheck the system.

6. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Ready to Upgrade** page, review the options, and select **Upgrade**.

8. When upgrade is finished, the **Upgrade complete** page appears. Select **Close**.

## To upgrade the Reporting server from the Command Prompt

1. Sign in to the computer that hosts the Reporting server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group.

2. Open an elevated Command Prompt by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager Setup.exe file is located, and run the following command:

    > [!NOTE]
    > If the Reporting server reports to an unsupported or inaccessible root management server, you must also pass the following parameter: `/ManagementServer: <ManagementServerName>`.

    ```
    setup.exe /silent /AcceptEndUserLicenseAgreement:1 /upgrade
    /ManagementServer: <ManagementServerName>

    ```

::: moniker-end

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
