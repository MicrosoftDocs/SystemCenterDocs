---
title: How to Upgrade an ACS Collector to System Center 2016 - Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97d62062-dda1-4841-aa7c-a7d6a5c7210f
---
# How to Upgrade an ACS Collector to System Center 2016 - Operations Manager
Perform this procedure to upgrade the Audit Collection Services \(ACS\) Collector to [!INCLUDE[omblue_1](Token/omblue_1_md.md)] locally on the ACS Collector. During this procedure, the ACS database is also upgraded without any additional steps.

> [!WARNING]
> A computer that hosts an ACS Collector must also be an [!INCLUDE[omblue_2](Token/omblue_2_md.md)] management server or gateway server.

Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements: System Center 2016 Operations Manager](System-Requirements-for-System-Center-Technical-Preview.md)

### To upgrade an ACS Collector

1.  Log on to the computer that hosts the ACS Collector with an [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Administrators role account for your [!INCLUDE[omblue_2](Token/omblue_2_md.md)] management group.

2.  On the [!INCLUDE[omblue_2](Token/omblue_2_md.md)] media, run **Setup.exe**.

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


