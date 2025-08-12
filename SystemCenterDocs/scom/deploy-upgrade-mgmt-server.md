---
ms.assetid: aabf9661-6b4c-4495-845d-7d30de3cff93
title: Upgrade a Management Server - Upgrade a Distributed Management Group
description: This article describes how to upgrade a management server in a distributed deployment of Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency.5, engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Upgrade a management server - upgrade a distributed management group

When you upgrade a distributed management group, you start by upgrading each of the management servers in your management group. There are many pre-upgrade tasks that you must perform first. For more information, see [Pre-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-overview.md).

> [!IMPORTANT]
> Between the time that you upgrade the management servers and upgrade the agents, you might experience Application Platform Monitoring (APM)-related event log entries on the agent-managed servers. These event log entries might occur on agent-managed servers that aren't APM-enabled. These event log entries will be resolved when you complete the upgrade of the agents. You might have to restart the health service after the agent is upgraded in order to clear the events.

> [!NOTE]
> Because the ACS Collector server must be on the same machine as a management server, we recommend you perform the steps described in [How to Upgrade an ACS Collector](~/scom/deploy-upgrade-acs-collector.md) along with the upgrade of the management server on which ACS resides.

> [!IMPORTANT]
> When upgrading multiple management servers in a distributed management group, you must wait to start upgrade of additional management servers until after the setup on the first management server completes. Failing to do so can cause a SQL update script that runs early in the set up process to run on multiple management servers and result in database issues. This SQL update script only needs to run on the initial management server being upgraded.

> [!NOTE]
> When upgrading multiple management servers in a distributed management group, sequence the upgrades in a manner that best suits your business needs. Upgrade all management servers in the distributed management group as soon as possible after the initial management server is upgraded to verify that your upgraded environment is healthy.

## Upgrade a management server

Follow these steps to upgrade a management server:

1. Sign in to the Operations Manager management server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2. From the Operations Manager media, run **Setup.exe**, and then select **Install**. The **Getting Started** page displays information about which features will be upgraded.

3. On the **Getting Started** page, select **Next** to proceed with the upgrade.

4. On the **Getting Started, Please read the license terms** page, read the Microsoft Software License Terms, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.

5. On the **Getting Started, Select installation location** page, accept the default value, enter a new location, or browse to one. Then select **Next**.

::: moniker range="<=sc-om-2022"
    
   > [!NOTE]
   > For System Center 2016 - Operations Manager, the default path is C:\Program Files\Microsoft System Center 2016\Operations Manager.  For all later releases (2019 and 2022), the default path is C:\Program Files\Microsoft System Center\Operations Manager.

::: moniker-end

::: moniker range="sc-om-2025"
   > [!NOTE]
   > For System Center 2025 - Operations Manager, the default path is C:\Program Files\Microsoft System Center\Operations Manager.

::: moniker-end

6. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify prerequisites again** to recheck the system.

7. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites, Proceed with Setup** page appears. Select **Next**.

8. On the **Configuration, Configure Operations Manager accounts** page, enter the domain account credentials for the System Center Configuration and Data Access Service account, and select **Next**

9. Review the **Configuration, Ready To Upgrade** page, and select **Upgrade**. The upgrade proceeds and displays the upgrade progress.

10. When the upgrade is finished, the **Upgrade complete** page appears. Select **Close**.

    > [!NOTE]
    > Upgrading a management server is just one phase of the distributed upgrade process. Upgrade isn't completed until you've upgraded all of the other features in your management group. The next step is to upgrade any gateways. For more information, see [How to Upgrade a Gateway Server](~/scom/deploy-upgrade-gateway-server.md).

## Upgrade a management server from the command prompt

Follow these steps to upgrade a management server from the command prompt:

1. Sign in to the management server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2. Open a command prompt window by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager setup.exe file is located, and run the following command:

    ```
    setup.exe /silent /upgrade
    /AcceptEndUserLicenseAgreement:1
    /DASAccountUser: <domain\username>
    /DASAccountPassword: <password>
    /DataReaderUser:<domain\user>
    /DataReaderPassword:<password>
    ```

After you've upgraded all of the management servers in your management group, you should upgrade gateway servers, and then upgrade any standalone Operations consoles.

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).  
