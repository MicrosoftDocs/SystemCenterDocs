---
title: How to Upgrade Reporting to System Center 2016 - Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4acce38-b84d-42af-8a41-b9464126cbc9
---
# How to Upgrade Reporting to System Center 2016 - Operations Manager
Use this procedure to upgrade a stand\-alone Reporting server to [!INCLUDE[scom_threshold_1](Token/scom_threshold_1_md.md)]. You should not run upgrade on the Reporting server until after you have upgraded the management servers, gateways, Operation consoles, and agents.

Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements: System Center 2016 - Operations Manager](System-Requirements-for-System-Center-Technical-Preview.md).

### To upgrade the Reporting server

1.  Log on to the computer that hosts the Reporting server with an account that is a member of the [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Administrators role for your [!INCLUDE[omblue_2](Token/omblue_2_md.md)] management group and the SQL Server sysadmin fixed server role.

2.  On the [!INCLUDE[omblue_2](Token/omblue_2_md.md)] source media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **System Center 2016 Operations Manager Upgrade** page, review the features that will be upgraded. In this case, it is [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Reporting. Click **Next**.

4.  On the **Select installation location** page, accept the default value of **C:\\Program Files\\ Microsoft System Center 2016\\Operations Manager**, or type in a new location or browse to one. Then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again** to recheck the system.

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Ready to Upgrade** page, review the options, and then click **Upgrade**.

8.  When upgrade is finished, the **Upgrade complete** page appears. Click **Close**.

### To upgrade the Reporting server by using the command prompt

1.  Log on to the computer that hosts the Reporting server with an account that is a member of the [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Administrators role for your [!INCLUDE[omblue_2](Token/omblue_2_md.md)] management group.

2.  Open a Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Setup.exe file is located, and run the following command:

    > [!NOTE]
    > If the Reporting server reports to an unsupported or inaccessible root management server, you must also pass the following parameter: `/ManagementServer: <ManagementServerName>`.

    ```
    setup.exe /silent /AcceptEndUserLicenseAgreement:1 /upgrade 
    /ManagementServer: <ManagementServerName>

    ```


