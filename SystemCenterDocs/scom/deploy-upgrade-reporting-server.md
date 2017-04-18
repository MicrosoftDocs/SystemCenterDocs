---
ms.assetid: ae000f5e-9d67-4d0d-b093-8d103dce2047
title: How to Upgrade Reporting to System Center 2016 - Operations Manager
description: This article describes how to upgrade the Reporting server to Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade Reporting to System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

Use this procedure to upgrade a stand-alone Reporting server to System Center 2016 - Operations Manager. You should not run upgrade on the Reporting server until after you have upgraded the management servers, gateways, Operation consoles, and agents.

Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center 2016 - Operations Manager](../orchestrator/system-requirements.md).

### To upgrade the Reporting server

1.  Log on to the computer that hosts the Reporting server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group and the SQL Server sysadmin fixed server role.

2.  On the Operations Manager source media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **System Center 2016 Operations Manager Upgrade** page, review the features that will be upgraded. In this case, it is Operations Manager Reporting. Click **Next**.

4.  On the **Select installation location** page, accept the default value of **C:\Program Files\ Microsoft System Center 2016\Operations Manager**, or type in a new location or browse to one. Then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again** to recheck the system.

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Ready to Upgrade** page, review the options, and then click **Upgrade**.

8.  When upgrade is finished, the **Upgrade complete** page appears. Click **Close**.

### To upgrade the Reporting server from the Command Prompt

1.  Log on to the computer that hosts the Reporting server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group.

2.  Open an elevated Command Prompt by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager Setup.exe file is located, and run the following command:

    > [!NOTE]
    > If the Reporting server reports to an unsupported or inaccessible root management server, you must also pass the following parameter: `/ManagementServer: <ManagementServerName>`.

    ```
    setup.exe /silent /AcceptEndUserLicenseAgreement:1 /upgrade 
    /ManagementServer: <ManagementServerName>

    ```

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](deploy-upgrade-post-tasks.md).

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.

