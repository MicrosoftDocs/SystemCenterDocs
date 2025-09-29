---
ms.assetid: ed1c51df-2507-4f34-b051-04540896ac17
title: Install an Audit Collection Services (ACS) Collector and Database
description: This article describes how to install the Operations Manager ACS collector and database.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.custom: engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install an Audit Collection Services collector and database

Use the following procedures to install an Audit Collection Services (ACS) collector and database and to start the service for the ACS collector computer. Perform the procedures on the computer that's designated as your ACS collector for System Center Operations Manager.

## Prerequsites

The ACS database runs on a supported version of Microsoft SQL Server. The Audit Collection Services Collector Setup wizard creates the ACS database on an existing installation of SQL Server. To complete the installation procedure, you must be a member of the Local Administrators group on both the ACS collector and ACS database computers. You must also be a database administrator on the ACS database. As a best practice for security, consider using **Run As** to perform this procedure.

## Important considerations

::: moniker range="sc-om-2019"

Operations Manager 2019 UR1 and later support a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you're installing it.

::: moniker-end

::: moniker range=">=sc-om-2022"

Operations Manager supports a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you're installing it.

::: moniker-end

## Install an ACS collector and an ACS database

1. Sign in to the server by using an account that has local administrative credentials.

2. On the Operations Manager installation media, run **Setup.exe**, and then select **Audit collection services**.

    For monitoring UNIX and Linux computers, select **Audit collection services for UNIX/Linux**.

    The **Audit Collection Services Collector Setup** wizard opens.

3. On the **Welcome** page, select **Next**.

4. On the **License Agreement** page, read the license terms. Select **I accept the agreement**, and then select **Next**.

5. On the **Database Installation Options** page, select **Create a new database**, and then select **Next**.

6. On the **Data Source** page, in the **Data source name** box, enter a name that you want to use as the Open Database Connectivity (ODBC) data source name for your ACS database. By default, this name is **OpsMgrAC**. Then select **Next**.

7. On the **Database** page, if the database is on a separate server than the ACS collector, select **Remote Database Server**, and then enter the computer name of the database server that will host the database for this installation of ACS. Otherwise, select **Database server running locally**.

8. In the **Database server instance name** field, enter the name of the server and the name of the SQL Server instance (if it isn't the default instance) for the database server that will host the ACS database.

9. In the **Database** name field, the default database name of **OperationsManagerAC** is automatically entered. You can select the text and enter a different name or leave the default name. Then select **Next**.

    > [!NOTE]
    > The database name can't contain the hyphen (`-`) character.

10. On the **Database Authentication** page, select one of the authentication methods. If the ACS collector and the ACS database are members of the same domain, you can select **Windows authentication**. Otherwise, select **SQL authentication**. Then select **Next**.

11. If you selected **SQL authentication** in the previous step, the **Database Credentials** page appears. In the **SQL login name** box, enter the name of the user account that has access to the SQL Server instance. In the **SQL password** box, enter the password for that account. Then select **Next**.

12. On the **Database Creation Options** page, select **Use SQL Server's default data and log file directories** to use the SQL Server default folders. Otherwise, select **Specify directories** and enter the full path, including drive letter, to the location that you want for the ACS database and log file. An example of a full path is `C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data`. Then select **Next**.

13. On the **Event Retention Schedule** page, select **Local hour of day to perform daily database maintenance**. Choose a time when the number of expected security events is low. During the database maintenance period, database performance is affected.

14. In the **Number of days to retain events** box, enter the number of days that ACS should keep events in the ACS database before the events are removed during database grooming. The default value is 14 days. Then select **Next**.

15. On the **ACS Stored Timestamp Format** page, choose **Local** or **Universal Coordinated Time**. Then select **Next**.

16. The **Summary** page displays a list of actions that the installation program will perform to install ACS. Review the list, and then select **Next** to begin the installation.

    > [!NOTE]
    > If a **SQL server login** dialog appears and the database authentication is set to **Windows authentication**, select the correct database and verify that the **Use Trusted Connection** checkbox is selected. Otherwise, clear the checkbox and enter the SQL Server sign-in name and password. Then select **OK**.

17. When the installation is complete, select **Finish**.

## Verify ACS collector performance

You can verify the ACS collector performance by using Performance Monitor or PowerShell.

### Monitor ACS collector performance data by using Performance Monitor

1. Sign in to the computer where Performance Monitor is installed.

2. On the **Run** page, enter **perfmon.msc**, and then select **OK**.

3. Under **Performance** > **Monitoring Tools**, right-click **Performance Monitor**, and then select **Properties**.

   :::image type="performance monitor" source="media/deploy-install-acs/performance-monitor.png" alt-text="Screenshot that shows selections for opening Performance Monitor properties.":::

   The **Performance Monitor Properties** page opens.

4. On the **Data** tab, select the available counters, and then select **Remove**.

   :::image type="data-remove" source="media/deploy-install-acs/data-remove.png" alt-text="Screenshot that shows selections for removing data.":::

5. Select **Add**.

   :::image type="add" source="media/deploy-install-acs/add.png" alt-text="Screenshot that shows the Add button.":::

6. In the **Add Counters** dialog, locate the **ACS Collector** counter. Select **Add >>**, and then select **OK** to confirm the properties.

   :::image type="add counters" source="media/deploy-install-acs/add-counters.png" alt-text="Screenshot that shows selections for adding a counter.":::

7. In the **Performance Monitor** wizard, select the dropdown arrow, and then select **Report** to switch to the report view.

   :::image type="report view" source="media/deploy-install-acs/report-view.png" alt-text="Screenshot that shows selections for opening the report view.":::

8. ACS performance data appears, as shown in the following example.

   :::image type="acs collector data report" source="media/deploy-install-acs/acs-collector-data-report.png" alt-text="Screenshot that shows the ACS collector data report.":::

### Monitor ACS collector performance data by using PowerShell

Use the following PowerShell commands to view the ACS collector performance data.

#### Example 1: Get a single sample of ACS collector performance counters

```powershell
Get-Counter -ListSet 'ACS Collector' | Get-Counter
```

#### Example 2: Get continuous samples of ACS collector performance counters

```powershell
Get-Counter -ListSet 'ACS Collector' | Get-Counter -Continuous
```

To stop the command, select <kbd>CTRL</kbd>+<kbd>C</kbd>.

To specify a longer interval (in seconds) between samples, use the `-SampleInterval` parameter.

The following screenshot shows example output.

:::image type="example" source="media/deploy-install-acs/example.png" alt-text="Screenshot that shows a PowerShell example for gathering ACS collector performance data.":::

## Deploy ACS reporting

1. On the server that will host ACS reporting, sign in as a user who's an administrator of the SQL Server Reporting Services instance.

2. Create a temporary folder, such as **C:\acs**.

3. On your installation media, go to **\ReportModels\acs** and copy the directory contents to the temporary installation folder.

    There are two folders (**Models** and **Reports**) and a file named **UploadAuditReports.cmd**.

4. On your installation media, go to **\SupportTools** and copy the file **ReportingConfig.exe** into the temporary **acs** folder.

5. Open a Command Prompt window by using the **Run as Administrator** option, and then change directories to the temporary **acs** folder.

6. Run the following command:

    `UploadAuditReports "<AuditDBServer\Instance>" "<Reporting Server URL>" "<path of the copied acs folder>"`

    The following example creates a new data source called **Db Audit**, uploads the reporting models **Audit.smdl** and **Audit5.smdl**, and uploads all reports in the **acs\reports** directory:

    `UploadAuditReports "myAuditDbServer\Instance1" "http://myReportServer/ReportServer$instance1" "C:\acs"`

    > [!NOTE]
    > The reporting server URL needs the reporting server virtual directory (`ReportingServer_<InstanceName>`) instead of the reporting manager directory (`Reports_<InstanceName>`).

7. In File Explorer, enter the following address to view the **SQL Reporting Services Home** page: `http://<yourReportingServerName>/Reports_<InstanceName>`.

8. Select **Audit Reports** in the body of the page, and then select **Show Details** on the upper-right part of the page.

9. Select the **Db Audit** data source.

10. In the **Connect Using** section, select **Windows Integrated Security**, and then select **Apply**.

## Related content

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed deployment of Operations Manager](deploy-distributed-deployment.md).  
