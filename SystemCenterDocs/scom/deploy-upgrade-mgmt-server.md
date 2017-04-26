---
ms.assetid: aabf9661-6b4c-4495-845d-7d30de3cff93
title: How to Upgrade a Management Server to System Center 2016 - Operations Manager -Upgrading a Distributed Management Group
description: This article describes how to upgrade a management server in a distributed deployment of Operations Manager 2016. 
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade a management server to System Center 2016 - Operations Manager - upgrading a distributed management group

>Applies To: System Center 2016 - Operations Manager

When you upgrade a distributed management group to System Center 2016 - Operations Manager, you start by upgrading each of the management servers in your management group. There are a number of pre-upgrade tasks that you must perform first. For more information, see [Pre-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](deploy-upgrade-overview.md).

> [!IMPORTANT]
> Between the time that you upgrade the management servers and upgrade the agents, you might experience Application Platform Monitoring (APM)-related event log entries on the agent-managed servers. These event log entries might occur on agent-managed servers that are not APM-enabled. These event log entries will be resolved when you complete the upgrade of the agents. You might have to restart the health service after the agent is upgraded in order to clear the events.

> [!NOTE]
> Because the ACS Collector server must be on same machine as a management server, we recommend you perform the steps described in [How to Upgrade an ACS Collector to System Center 2016 - Operations Manager](~/scom/deploy-upgrade-acs-collector.md) along with the upgrade of the management server on which ACS resides.

> [!IMPORTANT]
> When upgrading multiple management servers in a distributed management group, you must wait to start upgrade of additional management servers until after setup on the first management server completes. Failing to do so can cause a SQL update script that runs early in the set up process to run on multiple management servers and result in database issues.  This SQL update script only needs to run on the initial management server being upgraded.

> [!NOTE]
> When upgrading multiple management servers in a distributed management group, sequence the upgrades in a manner that best suits your business needs.  Upgrade all management servers in the distributed management group as soon as possible after the initial management server is upgraded to verify that your upgraded environment is healthy.

### To upgrade a management server

1.  Log on to the Operations Manager management server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2.  From the Operations Manager media, run **Setup.exe**, and then click **Install**. The **Getting Started** page displays information about which features will be upgraded.

3.  On the **Getting Started, System Center 2016 Operations Manager Upgrade** page, click **Next** to proceed with the upgrade.

4.  On the **Getting Started, Please read the license terms** page, read the Microsoft Software License Terms, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

5.  On the **Getting Started, Select installation location** page, accept the default value of **C:\Program Files\Microsoft System Center 2016\Operations Manager**, or type in a new location, or browse to one. Then click **Next**.

6.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify prerequisites again** to recheck the system.

7.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites, Proceed with Setup** page appears. Click **Next**.

8.  On the **Configuration, Configure Operations Manager accounts** page, enter the domain account credentials for the System Center Data Access Service account, and then click **Next**

9. Review the **Configuration, Ready To Upgrade** page, and then click **Upgrade**. The upgrade proceeds and displays the upgrade progress.

10. When the upgrade is finished, the **Upgrade complete** page appears. Click **Close**.

    > [!NOTE]
    > Upgrading a management server is just one phase of the distributed upgrade process. Upgrade is not completed until you have upgraded all of the other features in your management group. The next step is to upgrade any gateways.  See [How to Upgrade a Gateway Server to System Center 2016 - Operations Manager](~/scom/deploy-upgrade-gateway-server.md) for more information.

### To upgrade a management server from the Command Prompt

1.  Log on to the management server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2.  Open a Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    ```
    setup.exe /silent /upgrade 
    /AcceptEndUserLicenseAgreement:1
    /DASAccountUser: <domain\username>
    /DASAccountPassword: <password>
    /DataReaderUser:<domain\user>
    /DataReaderPassword:<password>
    ```

After you have upgraded all of the management servers in your management group, you should upgrade gateway servers, and then upgrade any stand-alone Operations consoles.


## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](deploy-upgrade-post-tasks.md).

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
