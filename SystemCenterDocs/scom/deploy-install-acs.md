---
ms.assetid: ed1c51df-2507-4f34-b051-04540896ac17
title: How to Install an Audit Collection Services ACS Collector and Database
description: This article describes how to install the Operations Manager Audit Collector and ACS database.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 02/11/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to install an Audit Collection Services (ACS) collector and database

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

Use the following procedures to install an Audit Collection Services (ACS) collector and database and to start the service for the ACS collector computer. Both procedures are performed on the computer that is designated as your ACS collector.

::: moniker range="sc-om-2019"

>[!NOTE]
> Operations Manager 2019 UR1 and later supports a single installer for all supported languages, instead of language specific installers. The installer automatically selects the language, based on the computer's language settings, where you are installing it.

::: moniker-end

The ACS database runs on a supported version of Microsoft SQL Server. The Audit Collection Services Collector Setup wizard creates the ACS database on an existing installation of Microsoft SQL Server. To complete the installation procedure, you must be a member of the local Administrators group on both the ACS collector and the ACS database computers as well as a database administrator on the ACS database. As a best practice for security, consider using Run As to perform this procedure.

## To install an ACS collector and an ACS database

1.  Log on to the server by using an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Audit collection services**.

    For monitoring UNIX and Linux computers, click **Audit collection services for UNIX/Linux**.

    The **Audit Collection Services Collector Setup** wizard opens.

3.  On the **Welcome** page, click **Next**.

4.  On the **License Agreement** page, read the licensing terms, click **I accept the agreement**, and then click **Next**.

5.  On the **Database Installation Options** page, click **Create a new database**, and then click **Next**.

6.  On the **Data Source** page, in the **Data source name** box, type a name that you want to use as the Open Database Connectivity (ODBC) data source name for your ACS database. By default, this name is **OpsMgrAC**. Click **Next**.

7.  On the **Database** page, if the database is on a separate server than the ACS collector, click **Remote Database Server**, and then type the computer name of the database server that will host the database for this installation of ACS. Otherwise, click **Database server running locally**.

8.  In the **Database server instance name** field, type the name of the server and the name of the SQL Server instance, if not the default instance, for the database server that will host the ACS database.  In the **Database** name field, the default database name of **OperationsManagerAC** is automatically entered. You can select the text and type in a different name or leave the default name. Click **Next**.

9. On the **Database Authentication** page, select one of the authentication methods. If the ACS collector and the ACS database are members of the same domain, you can select **Windows authentication**, otherwise select **SQL authentication**, and then click **Next**.

    > [!NOTE]
    > If you select **SQL authentication** and click **Next**, the **Database Credentials** page displays. In the **SQL login name** box, enter the name of the user account that has access to the SQL Server and the password for that account in the **SQL password** box, and then click **Next**.

10. On the **Database Creation Options** page, click **Use SQL Server's default data and log file directories** to use SQL Server's default folders. Otherwise, click **Specify directories** and enter the full path, including drive letter, to the location you want for the ACS database and log file, for example C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data. Click **Next**.

11. On the **Event Retention Schedule** page, click **Local hour of day to perform daily database maintenance**. Choose a time when the number of expected security events is low. During the database maintenance period, database performance will be impacted. In the **Number of days to retain events** box type the number of days ACS should keep events in the ACS database before the events are removed during database grooming. The default value is 14 days. Click **Next**.

12. On the **ACS Stored Timestamp Format** page, choose **Local** or **Universal Coordinated Time**, formerly known to as Greenwich Mean Time, and then click **Next**

13. The **Summary** page displays a list of actions that the installation program will perform to install ACS. Review the list, and then click **Next** to begin the installation.

    > [!NOTE]
    > If a **SQL server login** dialog box displays and the database authentication is set to **Windows authentication**, click the correct database and verify that the **Use Trusted Connection** check box is checked. Otherwise click to remove the check and enter the SQL login name and password. Click **OK**.

14. When the installation is complete, click **Finish**.

## Verify ACS collector performance

### Monitor ACS collector performance data with Performance monitor 

1. Log on to the computer that has Performance monitor installed. 

2. Enter **perfmon.msc** on the **Run** page and click **OK**. 

3. Under **Performance** > **Monitoring Tools**, right-click **Performance Monitor** > **Properties**. **Performance Monitor Properties** page opens. 

   :::image type="performance monitor" source="media/deploy-install-acs/performance-monitor.png" alt-text="Screenshot showing performance monitor.":::

4. Under **Data**, select the available counters and click **Remove**. 

   :::image type="data-remove" source="media/deploy-install-acs/data-remove.png" alt-text="Screenshot showing how to remove data.":::

5. Click **Add**.

   :::image type="add" source="media/deploy-install-acs/add.png" alt-text="Screenshot showing add.":::

6. **Add Counters** page opens. Locate the **ACS Collector** counter and click **Add >>** and then click **OK** to confirm the properties. 
   
   :::image type="add counters" source="media/deploy-install-acs/add-counters.png" alt-text="Screenshot showing the add counters.":::

7. On the **Performance Monitor** wizard, click the drop-down and select **Report** to change the view of the report.

   :::image type="report view" source="media/deploy-install-acs/report-view.png" alt-text="Screenshot showing the report view.":::

8. ACS performance data is displayed as follows: 

   :::image type="acs collector data report" source="media/deploy-install-acs/acs-collector-data-report.png" alt-text="Screenshot showing the acs collector data report.":::

### Monitor ACS collector performance data with PowerShell 

Use the below PowerShell commands to view the ACS collector performance data:

#### Example 1: Get a single sample of ACS collector performance counters

Get a single sample of ACS collector performance counter values using the below command.

```powershell
Get-Counter -ListSet 'ACS Collector' | Get-Counter 
```

#### Example 2: Get continuous samples of ACS collector performance counters

Get continuous samples of ACS collector performance counter values using the below command. 

To stop the command, press \<CTRL+C>\.

To specify a longer interval (in seconds) between samples, use the **SampleInterval** parameter.

```powershell
Get-Counter -ListSet 'ACS Collector' | Get-Counter -Continuous 
```
 
**Example Output**

:::image type="example" source="media/deploy-install-acs/example.png" alt-text="Screenshot showing the PowerShell example for gathering ACS collector performance data.":::

## To deploy ACS reporting

1.  Log on to the server that will be used to host ACS reporting as a user that is an administrator of the SSRS instance.

2.  Create a temporary folder, such as **C:\acs**.

3.  On your installation media, go to **\ReportModels\acs** and copy the directory contents to the temporary installation folder.

    There are two folders (**Models** and **Reports**) and a file named **UploadAuditReports.cmd**.

4.  On your installation media, go to **\SupportTools** and copy the file **ReportingConfig.exe** into the temporary **acs** folder.

5.  Open a Command Prompt window by using the **Run as Administrator** option, and then change directories to the temporary **acs** folder.

6.  Run the following command.
    `UploadAuditReports "<AuditDBServer\Instance>" "<Reporting Server URL>" "<path of the copied acs folder>"`
    For example: `UploadAuditReports "myAuditDbServer\Instance1" "http://myReportServer/ReportServer$instance1" "C:\acs"`

    This example creates a new data source called **Db Audit**, uploads the reporting models **Audit.smdl** and **Audit5.smdl**, and uploads all reports in the **acs\reports** directory.

    > [!NOTE]
    > The reporting server URL needs the reporting server virtual directory (`ReportingServer_<InstanceName>`) instead of the reporting manager directory (`Reports_<InstanceName>`).

7.  Open Internet Explorer and enter the following address to view the **SQL Reporting Services Home** page. `http://<yourReportingServerName>/Reports_<InstanceName>`

8.  Click **Audit Reports** in the body of the page and then click **Show Details** in the upper right part of the page.

9. Click the **Db Audit** data source.

10. In the **Connect Using** section, select **Windows Integrated Security** and click **Apply**.

## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
