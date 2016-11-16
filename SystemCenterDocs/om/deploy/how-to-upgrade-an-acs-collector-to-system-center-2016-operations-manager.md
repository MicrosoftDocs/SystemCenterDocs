---
ms.assetid: 11da2a90-3cf3-4983-a71f-1065a792374e
title: How to Upgrade an ACS Collector to System Center 2016   Operations Manager
description: This article describes how to upgrade an ACS Collector to Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade an ACS Collector to System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

Perform this procedure to upgrade the Audit Collection Services (ACS) Collector to System Center 2016 - Operations Manager locally on the ACS Collector. During this procedure, the ACS database is also upgraded without any additional steps.

> [!WARNING]
> A computer that hosts an ACS Collector must also be an Operations Manager management server or gateway server.

Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center 2016 - Operations Manager](../plan/system-requirements.md).

### To upgrade an ACS Collector

1.  Log on to the computer that hosts the ACS Collector with an Operations Manager Administrators role account for your Operations Manager management group.

2.  On the Operations Manager media, run **Setup.exe**.

3.  In the **Install** section, click **Audit Collection Services**. The Audit Collection Services Setup wizard starts.

4.  On the **Welcome to the Audit Collection Services Collector Setup Wizard** page, click **Next**.

5.  On the **Database Installation Options** page, select **Use an existing database**, and then click **Next**.

6.  On the **Data Source** page, type the name that you used as the Open Database Connectivity data source name for your ACS database in the **Data source name** box. By default, this name is **OpsMgrAC**. Click **Next**.

7.  On the **Database** page, if the database is on a separate server than the ACS Collector, click **Remote Database Server**, and then type the computer name of the database server that will host the database for this installation of ACS. Otherwise, click **Database server running locally**, and then click **Next**.

8.  On the **Database Authentication** page, select one authentication method. If the ACS Collector and the ACS database are members of the same domain, you can select **Windows authentication**; otherwise, select **SQL authentication**, and then click **Next**.

    > [!NOTE]
    > If you select **SQL authentication** and click **Next**, the **Database Credentials** page appears. Enter the name of the user account that has access to the SQL Server in the **SQL login name**  box and the password for that account in the **SQL password** password box, and then click **Next**.

9. The **Summary** page displays a list of actions that the installation program will perform to upgrade ACS. Review the list, and then click **Next** to begin the installation.

    > [!NOTE]
    > If a **SQL Server Login** dialog box appears and the database authentication is set to **Windows Authentication**, select the correct database, and then verify that the **Use Trusted Connection** check box is selected. Otherwise, clear it, enter the SQL Server login name and password, and then click **OK**.

10. When the upgrade is finished, click **Finish**.

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](post-upgrade-tasks-when-upgrading-to-system-center-2016-operations-manager.md).

- See [Distributed Deployment of Operations Manager](Distributed-Deployment-of-Operations-Manager.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  

