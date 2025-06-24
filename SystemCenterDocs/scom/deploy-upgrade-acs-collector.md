---
ms.assetid: 11da2a90-3cf3-4983-a71f-1065a792374e
title: Upgrade an ACS Collector
description: This article describes how to upgrade an ACS Collector to the latest version of System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency.5, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade an ACS Collector



Perform this procedure to upgrade the Audit Collection Services (ACS) Collector locally on the ACS collector. During this procedure, the ACS database is also upgraded without any additional steps.

> [!WARNING]
> A computer that hosts an ACS Collector must also be an Operations Manager management server or gateway server.

Before you begin the upgrade process, ensure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

To upgrade an ACS Collector, follow these steps:

1. Sign in to the computer that hosts the ACS Collector with an Operations Manager Administrators role account for your Operations Manager management group.

2. On the Operations Manager media, run **Setup.exe**.

3. In the **Install** section, select **Audit Collection Services**. The Audit Collection Services Setup wizard starts.

4. On the **Welcome to the Audit Collection Services Collector Setup Wizard** page, select **Next**.

5. On the **Database Installation Options** page, select **Use an existing database**, and select **Next**.

6. On the **Data Source** page, enter the name that you used as the Open Database Connectivity data source name for your ACS database in the **Data source name** box. By default, this name is **OpsMgrAC**. Select **Next**.

7. On the **Database** page, if the database is on a separate server than the ACS Collector, select **Remote Database Server**, and then enter the computer name of the database server that will host the database for this installation of ACS. Otherwise, select **Database server running locally**, and select **Next**.

8. On the **Database Authentication** page, select one authentication method. If the ACS Collector and the ACS database are members of the same domain, you can select **Windows authentication**; otherwise, select **SQL authentication**, and then select **Next**.

    > [!NOTE]
    > If you select **SQL authentication** and select **Next**, the **Database Credentials** page appears. Enter the name of the user account that has access to the SQL Server in the **SQL login name** box and the password for that account in the **SQL password** password box, and then select **Next**.

9. The **Summary** page displays a list of actions that the installation program will perform to upgrade ACS. Review the list, and then select **Next** to begin the installation.

    > [!NOTE]
    > If a **SQL Server Login** dialog appears and the database authentication is set to **Windows Authentication**, select the correct database, and then verify that the **Use Trusted Connection** check box is selected. Otherwise, clear it, enter the SQL Server login name and password, and select **OK**.

10. When the upgrade is finished, select **Finish**.

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
